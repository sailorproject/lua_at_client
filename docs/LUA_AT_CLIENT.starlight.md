# Usage Examples

Here are some examples of Lua code that will run on the browser using the `starlight` virtual machine:

##Manipulation of the DOM

    <div id="app"></div>
    <?lua@client
    
    local app = window.document:getElementById('app')
    print(app.textContent)
    app.textContent = 'lets go'
    
    window:alert('This code was written in Lua')
    
    ?>


##Accessing Javascript functions and passing callbacks


    <script>
    function myJSFunction(msg){
        console.log(msg);
    }

    function myJSFunctionReceivesCallback(callback){
        callback();
    }
    </script>

    <?lua@client
    window:myJSFunction('Calling a Javascript function from Lua')

    local function lua_callback()
        print('This is being printed from a Lua function being called in JS')
    end
    
    window:myJSFunctionReceivesCallback(callback)
    
    ?>

##Exporting Lua modules to the browser

Remember that this code will run on the browser and some Lua modules won't make sense being used in this context! Attention: this feature is still under tests.


    <?lua@client
    local valua = require "valua"
    -- If you installed Sailor, valua, its valuation module, was installed as a dependency
    
    local v = valua:new().len(3,10)
    print(v('Geronimo'))
    -- true
    ?>

##Accessing Javascript modules such as JQuery

    <script src="//code.jquery.com/jquery-1.11.3.min.js"></script>
    <script>
    function JQObj(s){
        return $(s);
        // This is necessary because the $() syntax will error on Lua
    }
    </script>

    <div id="app"></div>

    <?lua@client
    local app = window:JQObj('#app')
    app:html('This will be the new content of the div') 
    -- .html() is a JQuery function. Please observe that in Lua we will use the ':' notation
    ?>
