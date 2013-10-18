# Writing a JSLib Module

```javascript
SpilGames('spilgames.import', {
    name: 'ExampleModule',
    deps: ['dep1', 'dep2'],
    module: function(Dep1, Dep2) {
        'use strict';

        var foo     = 'bar',
            lorem   = 'ipsum',
            i;

        function doSomething(input) {
            var result = doSomethingElse(input);
            return result;
        }

        function doSomethingElse(bar) {
            return Dep1.get(bar) + lorem;
        }

        return {
            publicMethod: doSomething
        };
    }
});
```

# Writing a JSLib sandbox

```javascript
SpilGames(['dep1', 'dep2'], function(Dep1, Dep2) {
        'use strict';

        var arg = 'SpilGames';

        Dep1.publicMethod(arg);
    }
});
```
