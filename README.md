# NeatJSON
Pretty-print your JSON in Ruby with more power than is provided by `JSON.pretty_generate`.

## Installation

`gem install neatjson`

## Examples

~~~ ruby
require 'neatjson'

o = { b:42.005, a:[42,17], longer:true, str:"yes
please" }

puts JSON.neat_generate(o)
#=> {"b":42.005,"a":[42,17],"longer":true,"str":"yes\nplease"}

puts JSON.neat_generate(o,sorted:true)
#=> {"a":[42,17],"b":42.005,"longer":true,"str":"yes\nplease"}

puts JSON.neat_generate(o,sorted:true,padding:1,after_comma:1)
#=> { "a":[ 42, 17 ], "b":42.005, "longer":true, "str":"yes\nplease" }

puts JSON.neat_generate(o,sorted:true,wrap:40)
#=> {
#=>   "a":[42,17],
#=>   "b":42.005,
#=>   "longer":true,
#=>   "str":"yes\nplease"
#=> }

puts JSON.neat_generate(o,sorted:true,wrap:40,decimals:1)
#=> {
#=>   "a":[42.0,17.0],
#=>   "b":42.0,
#=>   "longer":true,
#=>   "str":"yes\nplease"
#=> }

puts JSON.neat_generate(o,sorted:true,wrap:40,aligned:true)
#=> {
#=>   "a"     :[42,17],
#=>   "b"     :42.005,
#=>   "longer":true,
#=>   "str"   :"yes\nplease"
#=> }

puts JSON.neat_generate(o,sorted:true,wrap:40,aligned:true,around_colon:1)
#=> {
#=>   "a"      : [42,17],
#=>   "b"      : 42.005,
#=>   "longer" : true,
#=>   "str"    : "yes\nplease"
#=> }

puts JSON.neat_generate(o,sorted:true,wrap:40,aligned:true,around_colon:1,short:true)
#=> {"a"      : [42,17],
#=>  "b"      : 42.005,
#=>  "longer" : true,
#=>  "str"    : "yes\nplease"}

a = [1,2,[3,4,[5]]]
puts JSON.neat_generate(a)
#=> [1,2,[3,4,[5]]]

puts JSON.pretty_generate(a) # oof!
#=> [
#=>   1,
#=>   2,
#=>   [
#=>     3,
#=>     4,
#=>     [
#=>       5
#=>     ]
#=>   ]
#=> ]

puts JSON.neat_generate( a, wrap:true, short:true )
#=> [1,
#=>  2,
#=>  [3,
#=>   4,
#=>   [5]]]
~~~

## Options
You may pass any of the following option symbols to `neat_generate`:

* `:wrap`           — The maximum line width before wrapping. Use `false` to never wrap, or `true` (or `-1`) to always wrap. Default: `80`
* `:indent`         — Whitespace used to indent each level when wrapping. Default: `"  "` (two spaces)
* `:short`          — Keep the output 'short' when wrapping? This puts opening brackets on the same line as the first value, and closing brackets on the same line as the last. Default: `false`
  * _This causes the `:indent` option to be ignored, instead basing indentation on array and object padding._
* `:sorted`         — Sort the keys for objects to be in alphabetical order? Default: `false`
* `:aligned`        — When wrapping objects, line up the colons (per object)? Default: `false`
* `:decimals`       — Decimal precision to use for numbers; use `false` to keep numeric values precise. Default: `false`
* `:array_padding`  — Number of spaces to put inside brackets for arrays. Default: `0`
* `:object_padding` — Number of spaces to put inside braces for objects.  Default: `0`
* `:padding`        — Shorthand to set both `:array_padding` and `:object_padding`. Default: `0`
* `:before_comma`   — Number of spaces to put before commas (for both arrays and objects). Default: `0`
* `:after_comma`    — Number of spaces to put after commas (for both arrays and objects). Default: `0`
* `:around_comma`   — Shorthand to set both `:before_comma` and `:after_comma`. Default: `0`
* `:before_colon`   — Number of spaces to put before colons. Default: `0`
* `:after_colon`    — Number of spaces to put after colons. Default: `0`
* `:around_colon`   — Shorthand to set both `:before_colon` and `:after_colon`. Default: `0`


## License & Contact

NeatJSON is copyright ©2015 by Gavin Kistner and is released under
the [MIT License](http://www.opensource.org/licenses/mit-license.php).
See the LICENSE.txt file for more details.

For bugs or feature requests please open [issues on GitHub][1].
For other communication you can [email the author directly](mailto:!@phrogz.net?subject=NeatJSON).


## TODO (aka Known Limitations)

* Fix bug with `short:true` and wrapping, nested objects.
* Figure out the best way to play with custom objects that use `to_json` for their representation.
* Option for `around_colon` to only apply to multi-line objects.
* Detect circular references.
* Possibly allow illegal JSON values like `NaN` or `Infinity`.

[1]: https://github.com/Phrogz/NeatJSON/issues