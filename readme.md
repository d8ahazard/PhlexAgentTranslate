#INSTRUCTIONS

##Adding a new translation:
1. Fork this repository.
2. Make a copy of the EN_DO_NOT_CHANGE directory.
3. Rename it to XX_translated, where XX is one of de (German), es (Spanish), fr (French), it(Italian), or ja (Japanese).
4. Translate ALL strings in the files to the best of your ability.
5. If adding new phrases, place them after the original strings.
6. Commit your changes.
7. Submit a pull request.
8. ???
9. PROFIT. 

##Translating individual files
Each file is a JSON file that contains trigger phrases used by API.ai.
For example, the file FR_needs_translation/entities/Controls_frtries_fr.json

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