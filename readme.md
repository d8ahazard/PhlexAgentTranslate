#INSTRUCTIONS

##Adding a new translation:
1. Fork this repository.
2. Review all files in entities and intents that end in the langauge you're translating (de,es,fr,ja,it).
3. If adding new phrases, place them after the original strings.
4. Commit your changes.
5. Submit a pull request.
6. ???
7. PROFIT. 

##Translating individual files
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

