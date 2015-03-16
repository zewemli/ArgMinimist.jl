# ArgMinimist

[![Build Status](https://travis-ci.org/zewemli/ArgMinimist.jl.svg?branch=master)](https://travis-ci.org/zewemli/ArgMinimist.jl)

ArgMinimist
================

Inspired by the [minimist](https://www.npmjs.com/package/minimist#readme) package for Node.js, this package strives to provide a simple and minimal argument parsing alternative to [ArgParse](https://github.com/carlobaldassi/ArgParse.jl).

How do I use it?
------------------

Try this:

<pre><code>
using ArgMinimist

positional, keyword = parse_args()
println(join(positional, " "))

for (sym, value) in keyword
  println("$(sym) == $(value)")
end
</code></pre>

Or if you know the arguments you want to get:
<pre><code>
using ArgMinimist

positional, keyword = parse_named_args(["arg1","arg2"])
println(join(positional, " "))

for (sym, value) in keyword
  println("$(sym) == $(value)")
end
</code></pre>

Argu-magic?
------------------

Positional arguments are returned in a Vector{Any}, keyword arguments are in a Dict{Symbol,Any}.
If a value looks like an integer, you get an integer. If it looks like a float you get a float. Otherwise you get a string.

Argument behaviors:

* Flags: -ab => keyword[:a] == true and keyword[:b] == true
* Long flags: --with-name => keyword[:name] == true
* More long flags: --name [nothing else] or --name --other-argument => keyword[:name] == true
* Negatives: --no-name => keyword[:name] == false
* Names: --name=bob or --name bob => keyword[:name] == "bob"

All other arguments get dumped into the positional argument array.

Got Defaults?
------------------

Calling parse_args! or parse_named_args! with a Dict{Symbol,Any} as the last argument will
put keyword arguments into the provided dictionary.
