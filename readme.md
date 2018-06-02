# INSTRUCTIONS

## Adding a new translation:
1. Fork this repository.
2. Review all files in entities and intents that end in the langauge you're translating (de,es,fr,ja,it, etc.).
3. If adding new phrases, place them after the original strings.
4. Commit your changes.
5. Submit a pull request.
6. ???
7. PROFIT. 

## Translating Entity Files
Each file is a JSON file that contains trigger phrases used by API.ai.
For example, the file /entities/Controls_entries_fr.json

It has multiple arrays like so:

    "value": "Resume",
    "synonyms": [
    "Resume",
    "Start",
    "Continue",
    "Resume Playback",
    "Unpause"

**The "value" portion should not change.**

But they synonyms - those need to be translated to french.

So, a translated array may look like this when done:

    "value": "Resume",
    "synonyms": [
    "CV",
    "Début",
    "Continuer",
    "Reprendre la lecture",
    "Unpause",
    "French-specific phrase meaning 'unpause'"...

Once all arrays are translated, save and commit.


## Translating Intent Files
Intent files are a bit more complicated to translated
Each intent contains a series of usersays_<LANG>.json files, where <LANG> is the target language.

Within the usersays files are multiple blocks of JSON, like so:

`
{
        "data": [
            {
                "text": "buscar",
                "alias": "controls",
                "meta": "@controls",
                "userDefined": false
            },
            {
                "text": " a ",
                "userDefined": false
            },
            {
                "text": "1 hora y 10 minutos",
                "alias": "duration",
                "meta": "@sys.duration",
                "userDefined": false
            }
        ]
    }
`

This JSON is an auto-translated representation of how the application will parse the phrase "seek to 1 hour and 10 minutes" in Spanish.

Because this phrase had to be translated one component at a time, the syntax of the sentence is not correct, and apparently, should actually be "busca 1 hora y 10 minutos".

So, to 'fix' this string, we would edit the JSON so it looks like this:

`
{
        "data": [
            {
                "text": "busca",
                "alias": "controls",
                "meta": "@controls",
                "userDefined": false
            },
            {
                "text": " ",
                "userDefined": false
            },
            {
                "text": "1 hora y 10 minutos",
                "alias": "duration",
                "meta": "@sys.duration",
                "userDefined": false
            }
        ]
    }
`

ALSO, we need to make sure that the word "busca" exists in the 'controls' entity file as a synonym for the command 'seek', because we replaced it with 'buscar'. Fun, right??

In this example, we just removed the " a " from the sentence, and replaced it with a space, **which is important**. It's annoying,
and it's also the reason I wasn't able to have my auto-translate bot do this for me.


A more complex (and nonsensical example) - Say the syntax of Spanish actually dicatated that we put the verb **after** the time - '1 hora y 10 minutos a busca'.

(I know that's awful, but it's just for example's sake)

Then, we would correct the JSON to look like this:

`
{
        "data": [
			{
                "text": "1 hora y 10 minutos",
                "alias": "duration",
                "meta": "@sys.duration",
                "userDefined": false
            },
            {
                "text": " a ",
                "userDefined": false
            },
            {
                "text": "busca",
                "alias": "controls",
                "meta": "@controls",
                "userDefined": false
            }
        ]
    }
`

Here, we've re-arranged the individual JSON blocks so that the syntax matches what we want it to be. Again, there need to be defined spaces between the target words, and 'busca' 
needs to exist in the controls entity file as a synonym for 'seek'.

You can obviously use the '_en.json' files as a reference, as these are the source files for the translation. Be aware that some examples may not exist for a target language,
as some of the @sys. meta types of entities (system entities) don't exist for all languages, and have been removed accordingly. 

As a side note - it would *really* be ideal to create our own entity arrays to replace these missing @sys items, as some commands just won't be available without them.


## Translating Flex TV /lang files

The files in the /lang directory should be a little easier to work with.

The majority of them are just key->value pairs, with the key being the reference that Flex TV uses to look up that translated string, and the value being the language-specific
version of the sample.

There are some exceptions, however. Some of the speech responses are *arrays* of examples, so that responses to the user may be randomized, and conversation seems more natural.

Regardless, when complete, the Language files for Flex TV should have 1:1 equivalent where ever possible.