# AAE2XMP
Script to convert AAE files (iOS media sidecar) to XMP (Lightroom sidecar)

Sources that can be helpful:
- https://github.com/nst/iOS-Runtime-Headers/blob/master/PrivateFrameworks/PhotosFormats.framework/PFAssetAdjustments.h
- https://github.com/neilpa/photohack
- https://github.com/RhetTbull/osxphotos

Plan:
1. collect AAE and XMP properties.
   - Sources for AAE:
     - AAE files from my iPhone (SE gen 2, iOS 16.1.1)
     - example files from https://stackoverflow.com/questions/61023739/decoding-adjustmentdata-in-aae-files-of-pictures-taken-by-the-iphone
   - Sources for XMP:
     - XMP files from Lightroom 9.2.1 library
     - TODO
3. try to pair them up --> create a table
4. find out a general algorithm that can be parametrized to convert between any pairs
   1. combine input values (AAE properties) if needed
   2. linear conversion or enumeration
   3. generate string representation of the resulted number (integer/fixed point/enumeration)
   4. add prefix and postfix

### Collecting AAE and XMP properties
To analyze my files I would like to combine them to see overall results. Two kind of set-like operations are used:
- intersection: elements common to all analyzed files
- union: all existing elements in all files

The analysis algorithms are written for XML but AAE has some challenges:
- Contains multiple key-value tag pairs. This makes order of tags important. Solution: convert to JSON with plistlib (?)
- Contains encoded JSON adjustmentData. Solution: decode then merge to the created JSON above

And then convert the final JSON to XML using ??? (TODO)

XML challenges:
- Same sibling tags: they can be unordered so we have to find pairs
- Same attribute multiple times: I don't think it would be valid XML so this won't be handled
- I would like to keep the order and formatting of the input files to make comparisons easy but I think it is impossible when handling the above situations.

#### How to combine XML elements

| element/pattern | intersection | union |
|-----------------|--------------|-------|
| XML tag / JSON key<br>non-repeating<br>no attributes | If same tag exist in both inputs (at the same point in tree structure), the tag is included in the result.<br>If tag exists only in one input, the tag is not included in  the result. | Tag is included in the result. |
| Same attribute with different values | Result is attribute without value | Result is attribute with set of possible values (notation can be value1 \| value2) |
| Same attribute exists multiple times | Not supported --> error in log. Fallback: if needed, included only once in the result. | Not supported --> error in log. Fallback: if needed, included only once in the result. |
| Tag exists multiple times | TODO: algorithm to find pairs<br>Tag without pair is not included in the result | TODO: algorithm to find pairs<br>Tag without pair is included in the result |
  

### AAE - XMP pairing results (ongoing)

| AAE                                                            | AAE representation | XMP | XMP representation | description |
|----------------------------------------------------------------|--------------------|-----|--------------------|-------------|
| adjustmentBaseVersion
| adjustmentData / metadata / masterHeight
| adjustmentData / metadata / masterWidth
| adjustmentData / metadata / orientation
| adjustmentData / formatVersion
| adjustmentData / versionInfo / buildNumber
| adjustmentData / versionInfo / appVersion
| adjustmentData / versionInfo / schemaRevision
| adjustmentData / versionInfo / platform
| adjustmentData / adjustments / ...                             | -                  | -   | -                 | multiple adjustments are possible, they are in an array
| adjustmentData / adjustments / # / formatVersion
| adjustmentData / adjustments / # / enabled
| adjustmentData / adjustments / # / settings / yaw
| adjustmentData / adjustments / # / settings / originalCrop
| adjustmentData / adjustments / # / settings / xOrigin
| adjustmentData / adjustments / # / settings / smart
| adjustmentData / adjustments / # / settings / width
| adjustmentData / adjustments / # / settings / yOrigin
| adjustmentData / adjustments / # / settings / straightenAngle
| adjustmentData / adjustments / # / settings / auto
| adjustmentData / adjustments / # / settings / height
| adjustmentData / adjustments / # / settings / constraintHeight
| adjustmentData / adjustments / # / settings / constraintWidth
| adjustmentData / adjustments / # / settings / pitch
| adjustmentData / adjustments / # / identifier
| adjustmentData / adjustments / # / formatIdentifier
| adjustmentEditorBundleID
| adjustmentFormatIdentifier
| adjustmentFormatVersion
| adjustmentRenderTypes
| adjustmentTimestamp
| found in older version of adjustmentData (base64 encoded bplist):
| adjustmentData / slowMotion / regions / ...                             | -                  | -   | -                 | multiple regions are possible, they are in an array
| adjustmentData / slowMotion / regions / # / timeRange / start / flags
| adjustmentData / slowMotion / regions / # / timeRange / start / value
| adjustmentData / slowMotion / regions / # / timeRange / start / timescale
| adjustmentData / slowMotion / regions / # / timeRange / start / epoch
| adjustmentData / slowMotion / regions / # / timeRange / duration / flags
| adjustmentData / slowMotion / regions / # / timeRange / duration / value
| adjustmentData / slowMotion / regions / # / timeRange / duration / timescale
| adjustmentData / slowMotion / regions / # / timeRange / duration / epoch
| adjustmentData / slowMotion / rate
