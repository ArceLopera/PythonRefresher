``` py
pip install emoji
pip install rich
print('\N{JUGGLING}') #Unicode Name
print('\U0001F939')#Unicode Codepoint
print('🤹') #Literal Character

import emoji, rich
print(emoji.emojize(':person_juggling:')) #pip install emoji
rich.print(':person_juggling:') #pip install rich
```
```
🤹
🤹
🤹
🤹
🤹
```