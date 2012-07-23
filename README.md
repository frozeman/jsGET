jsGET
==============================================
Copyright (C) Fabian Vogelsteller [frozeman.de]

published under the MIT-License
_____________________________________________

### AUTHOR
Fabian Vogelsteller <http://frozeman.de>

### DESCRIPTION
jsGET is a http GET-Variables clone for javascript, using the hash part of the URL (index.html#...).
You can set and get variables, and run a listener to hash changes, e.g. when the the history back button gets pressed.
This allows you to create a usable history navigation in your ajax application. It should work with all A-grade browsers.

### VERSION
0.2

### INSTALLATION
Just include the jsGET.js in your website/webapplication and use the jsGET object with its methods to set, get, remove history hash variables.
See the demo.html for examples.

### Properties
- vars:                     (object) the hash variables object loaded by get(), set(), remove(), or clear() or load() plus various indicators and trackers:
- vars.current:             (object) the current variables.
- vars.old:                 (object) the old variables, before they where changed with set(), remove(), clear() or the browser history back button.   *WARNING*: this is one is only valid while the listener is invoked.
- vars.changed:             (object) the variables which have changed since the last call of get(), set(), remove(), clear(), load() or the browser history back button.   *WARNING*: this is one is updated by setChangedVars() depending on 'vars.old' and usually is only valid while the listener is invoked.
- vars.change_count:        (integer) a number of variables changed/added/removed since the last time the listener was invoked.   *WARNING*: this is one is updated by setChangedVars() depending on 'vars.old' and usually is only valid while the listener is invoked.
- vars.last_hash_loaded:    (string, internal use only) the raw hash string which was just processed; in the listener, this equals the current hash.
- vars.last_hash_saved:     (string, internal use only) the hash section string which was the last one generated by set(), clear() or remove().
- vars.foreign_hash_change: (boolean) TRUE when the hash was changed from outside our control, e.g. when the user hit the 'back/history' button in the browser, after the previous invocation of the listener.
- vars.hash_changed:        (boolean) TRUE when the hash has changed after the previous invocation of the listener.

### Methods
- load():                                 loads the current hash variables into the vars.current property as JSON object. Return the updated set of key/value pairs.
- clear():                                clears the hash part of the URL. (because it's not completely possible, it sets it to "#_")
- get(get):                               (string) try to get a hash variable with the given name.
- set(set):                               (string,object) sets the given parameters to the hash variables. If it's a string it should have the following format: "key=value". Return the updated set of key/value pairs.
- remove(remove):                         (string,array) the variable name(s) which should be removed from the hash variables. Return the old set of key/value pairs.
- addListener(listener,callAlways,bind):  (listener: function, callAlways: boolean, bind: object instance) creates a listener which calls the given function when a hash change occurs. The called function will get the vars property (vars.current,vars.old,vars.changed) and use the "bind" parameter as "this", when specified.
  The return of the addListener() method is a setInterval ID and must be passed to the removeListener() method to stop the listening.
  When callAlways is FALSE, it only calls when the browser history buttons are pressed and not when get(), set(), remove() or clear() is called.
- removeListener(listenerID):             (the setInterval Id received from a addListener() method) removes a listener set with the addListener() method.
- setChangedVars():                       (internal use) updates the vars.changed collection and vars.change_count value.

### ATTENTION!
Everytime you call set(), remove() or clear() a new hash string will be set,
that means you also create a new history step in the browser history!

These are 'special' characters to jsGET and will therefor be encoded when they are part of a key or value:

>  # & =

