# AAE2XMP
Script to convert AAE files (iOS media sidecar) to XMP (Lightroom sidecar)

Sources that can be helpful:
- https://github.com/nst/iOS-Runtime-Headers/blob/master/PrivateFrameworks/PhotosFormats.framework/PFAssetAdjustments.h
- https://github.com/neilpa/photohack
- https://github.com/RhetTbull/osxphotos

Plan:
1. collect AAE and XMP properties.
   - Sources for AAE:
     - an AAE file from my iPhone (SE gen 2, iOS 16.1.1)
     - example files from https://stackoverflow.com/questions/61023739/decoding-adjustmentdata-in-aae-files-of-pictures-taken-by-the-iphone
   - Sources for XMP:
     - an XMP file from Lightroom 9.2.1
     - TODO
3. try to pair them up --> create a table
4. find out a general algorithm that can be parametrized to convert between any pairs
   1. combine input values (AAE properties) if needed
   2. linear conversion or enumeration
   3. generate string representation of the resulted number (integer/fixed point/enumeration)
   4. add prefix and postfix

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
