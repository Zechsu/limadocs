LIMA Mudlib spellmaking
============

Inheritables
***************
Depending on the usage, there are only two types of spell inheritables. ``SPELL`` and ``COMBAT_SPELL``. The difference between those is that ``COMBAT_SPELL`` is a source of damage and are used to inflict damage. In either case, all spells must inherit ``SPELL`` in order to work. Only if they're supposed to do damage, should they also inherit ``COMBAT_SPELL``.

SPELL
===============
A most simple spell will consist of 2 functions. ``setup()`` and ``cast_spell()``. Normally ``setup()`` should only set the name of the spell using ``set_spell_name(string s)`` and ``cast_spell(object ob, object reagent)`` will contain the logic which is executed when the spell is cast.

.. note::
   When a spell's object is loaded, the constructor automatically calls ``SPELL_D`` to register it.

set_spell_name(string s)
------------------------

``set_spell_name()`` set's the spell's name. This is for the cast verb and also for registering in ``SPELL_D``. Should be called in ``setup()``.

valid_target(object target)
---------------------------

``valid_target(object target)`` returns 1 by default. Should return 1 if target is valid, otherwise return 0. This should be used for checking if the target's of the valid type. For example: ``if (target->is_lockable())``.

valid_reagent(object reagent)
-----------------------------

``valid_reagent(object reagent)`` returns 0 if a reagent is given. This is so because most spells probably won't need a reagent. Otherwise return 1 after checking if the reagent is correct.

valid_circumstances(mixed target, mixed reagent)
------------------------------------------------

``valid_circumstances(mixed target, mixed reagent)`` returns 1 by default. Should return 1 if the spell's casting is possible, otherwise return 0. This should check for circumstances such as if the target or reagent have been given ``if (target)`` or ``if (reagent)``, but not check if they're valid types. That should be done in the ``valid_target`` and ``valid_reagent`` functions.

.. note::
   Can also be used for checking if the player's in the correct guild.

cast_spell(object target, object reagent)
-----------------------------------------

``cast_spell(object target, object reagent)`` contains all the logic of what happens when the spell is cast.
