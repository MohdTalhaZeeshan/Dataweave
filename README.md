# Dataweave
%dw 2.0
output application/json
var x = payload splitBy  " "
var y = x filter ((item, index) -> item contains  /[0-9]/ )
---
{
    "num" : y[0],
    "alpha" : payload replace  /[0-9]/ with ""  or  payload replace  /[^A-Za-z]/ with ""
}
output :
{
  "num": "123",
  "alpha": "Hello  World"
}


%dw 2.0
import * from dw::core::Strings
output application/json
---
{
    "Num": payload filter (isNumeric($) ),
    "Alpha": payload filter (isAlpha($) )
}
