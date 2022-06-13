# Scripting Basics

Once you have ev-as setup per the readme in the [repository](https://github.com/z80rotom/ev-as) I also highly recommend [Visual Studio Code](https://code.visualstudio.com/) and the [language support for evscript extension](https://marketplace.visualstudio.com/items?itemName=Heroj04.bdsp-evscript-language-support).

Reminder: You want to edit the scripts in the `scripts` folder, not parsed. If you don't have a scripts folder, make one and paste your parsed scripts here.

Also, when copying over your script changes to your emulator/switch for testing, you want to take the `ev_scripts` file from the `bin` folder, not `Dpr`, as `Dpr` will not have the changes.

Now you have the context on how to get your scripts interacting with the game, lets get to adding things.

## Baby steps
For our first attempt at scripting, we will change what an NPC says. Open VSC (Visual Studio Code)

In `c01.ev`, which is Jubilife external's scripts. Find `ev_c01_woman3` which should have a function body of 
```
_EASY_OBJ_MSG('dp_scenario1%27-msg_c01_woman3_01')
END()
```

The message is being called as such, in the `dp_scenario1` file, find `27-msg_c01_woman3_01` with `%` being used as a separator. 

Back in the early days of scripting, we had to use tooling to create new messages in these files, but thankfully, with the addition of macros, you no longer need to do this.
Most dialogue commands have been extends to have what is known as a "Macro" variant, which you can pass the string of text to what you want to be displayed as dialogue. In this instance,  it would be `_MACRO_EASY_OBJ_MSG`.

Now what do we do? That's easy, you simply change the current `_EASY_OBJ_MSG` line to the following.

`_MACRO_EASY_OBJ_MSG('dp_scenario1', '27-msg_c01_woman3_01', 'Spinda is the best Pokémon ever.')`

Now all you need to do is save and compile your new script. I personally use `python3 src/ev_as.py` with my setup.

Once that completes (you may need to provide the dp_scenario1 message file in another folder).  Simply take `bin\ev_script` and put it in your mod folder in `Dpr`.