The Chargen object stores all the commands used to set different character attributes, such as skill bonuses. It is intended to be used as a @parent, with 'Chargen Rooms' being @set WIZARD and @parented to it.

The most variable part of the Chargen object is the DATA`STUNTS`* attribute tree.

@@ On the chargen object, the attributes in the tree 'data`stunts`lists`<category>' (e.g. data`stunts`lists`toughness) will store the code for those actual stunts. Format: codename~showname~cost~note~test~buy~del|nextstunt.
@@ test, buy, and del each store code which will be evaluated at those times. If they start with ':', then the rest will be the name of an attribute (on the chargen object, within the data`stunts`* tree) which will be used. Otherwise, that string is itself treated as code. This code must use side-effect functions instead of commands.
@@ The 'test' code must be written as if it begins with 'switch(0,' and ends with a <dflt> that will activate the actual stunt-buying code. %2 will glob everything after the second = sign.
@@ The 'del' code must be escaped once, so that %qX substitutions can work.