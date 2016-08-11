# Ruby

*RubyGems* - package management system.


``to_s`` converts values to **s**trings

``to_i`` converts values to **i**ntegers

``to_a`` converts values to **a**rrays

**Exclamation Points.** Methods may have exclamation points in their name, 
which just means to impact the current data, rather than making a copy.

``ticket.sort!`` The exclamation signals that we intend for Ruby to directly 
modify the same array that we've built, rather than make a brand new copy 
that is sorted.

**Square Brackets.** With these, you can target and find things. 
You can even replace them if necessary.

**Chaining methods** lets you get a lot more done in a single command. 
Break up a poem, reverse it, reassemble it: ``poem.lines.to_a.reverse.join``.

[Complete list of string methods](http://ruby-doc.org/core-2.3.0/String.html)
