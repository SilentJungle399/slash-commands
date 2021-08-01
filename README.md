# slash-commands
Since this is for personal use, it will not be published on pypi.

## Installation and Usage

To install this module, run 
```bash
pip install -U git+https://github.com/SilentJungle399/slash-commands.git
```

### Usage

I'm not going to write a documentation on this thing, people who are curious can go through the code.

For a headstart, I'll provide an example here

```py
from slash import *
from discord.ext import commands

bot = commands.Bot(command_prefix=commands.when_mentioned_or('?'))
bot.slashclient = SlashClient(bot)

class Blep(SlashCommand):
	def __init__(self):
		super().__init__(
			bot.slashclient, 
			name="blep", 
			description = "Some blep description",
			# A reference to discord docs for options
			# https://discord.com/developers/docs/interactions/slash-commands#application-command-object-application-command-option-structure
			options = [
				{ 
					"type": 3,
					"name": "pleb",
					"description": "some pleb description",
					"required": False
				}
			]
		)

	async def callback(self, ctx: InteractionContext):
		await ctx.reply(f"why {ctx.data['options'][0]['value']}", ephemeral=True)

@bot.event
async def on_ready():
	print(f'Logged on as {bot.user} (ID: {bot.user.id})')
	await bot.slashclient.add_command(Blep())

bot.run("TOKEN")
```

### Screenshots
![image](https://user-images.githubusercontent.com/75272148/127775083-6722865b-b38a-4c1c-aeab-67792448224b.png)

![image](https://user-images.githubusercontent.com/75272148/127775088-8504cd9d-0b94-4e82-a683-e8acb6cc0f43.png)

![image](https://user-images.githubusercontent.com/75272148/127775094-75c435c7-6600-4a43-9433-80482692821f.png)
