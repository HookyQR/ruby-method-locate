# ruby-method-locate
[![Build Status](https://travis-ci.org/HookyQR/ruby-method-locate.svg?branch=master)](https://travis-ci.org/HookyQR/ruby-method-locate)

Finds position of ruby methods/modules/classes in a file. Intended for use in code editors.

```javascript
const rubyLocate = require('ruby-method-locate');

rubyLocate('./main.rb').then(result => {
  // ...
}).catch( failure => {
  // some file access error
});
```

If `main.rb` contains:

```ruby
module Module
  class Class
    def initialize
    end

    def call
    end
  end
end
```

the locator will return a promise which resolves with:
```javascript
{ '{/ABSOLUTE/PATH/TO/}/basic.rb':
   { module:
      { Module:
         { posn: { line: 0, char: 7 },
           class:
            { Class:
               { posn: { line: 1, char: 8 },
                 method:
                  { initialize: { posn: { line: 2, char: 8 } },
                    call: { posn: { line: 5, char: 8 } }
                  } } } } } } }
```