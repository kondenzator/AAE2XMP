# AAE2XMP
Script to convert AAE files (iOS media sidecar) to XMP (Lightroom sidecar)

Plan:
1. collect AAE and XMP attributes
2. try to pair them up --> create a table
3. find out a general algorithm that can be parametrized to convert between any pairs
   1. combine input values
   2. linear conversion or enumeration
   3. generate string representation of the resulted number (integer/fixed point/enumeration)
   4. add prefix and postfix

| AAE | AAE representation | XMP | XMP representation | description |
|-----|--------------------|-----|--------------------|-------------|
| adjustmentBaseVersion
| adjustmentData / metadata / masterHeight
| adjustmentData / metadata / masterWidth
| adjustmentData / metadata / orientation
| adjustmentData / formatVersion
| adjustmentData / versionInfo / buildNumber
| adjustmentData / versionInfo / appVersion
| adjustmentData / versionInfo / schemaRevision
| adjustmentData / versionInfo / platform
| adjustmentData / adjustments / ...
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
