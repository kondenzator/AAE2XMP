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
