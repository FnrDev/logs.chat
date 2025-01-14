# Chat Logs

<center>
	<a href="https://nodei.co/npm/logs.chat/">
		<img alt="Chat Logs NPM Package Statistics" src="https://nodei.co/npm/logs.chat.png">
	</a>
</center>

* NPM package that saves messages online to view it later
* Useful for bots where users can save messages history & cleared messages online
* Supports the Promise-API, you will be able to use .then, .catch, etc...

<center>
	<img style="border-radius: 7px;" alt="Example Picture" src="https://logs.chat/img/example1.png">
	<a href="https://logs.chat/chat/1" target="_blank">
		<img style="border-radius: 7px;" alt="Example Picture" src="https://logs.chat/img/example2.png">
	</a>
</center>

Check out or website [Chat Logs](https://logs.chat).

# Installation from [NPM](https://www.npmjs.com/package/logs.chat)

`npm i logs.chat`

# Usage

- `create(messages)` - Saves chat messages online
    - `messages`: (REQUIRED) Discord Chat Messages Collection
- `get(id)` - Gets a saved chat messages
    - `id`: (REQUIRED) Chat ID
- `exists(id)` - Check if a saved chat exists
    - `id`: (REQUIRED) Chat ID

##
it will return an object looks like this:
```json
{
	"ID": "1",
	"url": "https://logs.chat/chat/1"
}
```

## Example

```js
const chat = require('logs.chat');
const Discord = require('discord.js');
const client = new Discord.Client({
	"intents": [
		"GUILDS",
		"GUILD_MESSAGES"
	]
});
const prefix = '!';

client.on('ready', () => {
	console.log('Logged in as ' + client.user.tag);
});

client.on('messageCreate', async message => {
	if (!message.content.startsWith(prefix) || message.author.bot) return;

	const args = message.content.slice(prefix.length).trim().split(/ +/);
	const command = args.shift().toLowerCase();

	if (command === 'save') {
		let messages = await message.channel.messages.fetch();
		let createdChat = await chat.create(messages);
		let embed = new Discord.MessageEmbed()
			.setTitle(`Chat Created with ${messages.size} messages`)
			.setColor("#00bd8d")
			.setThumbnail(message.guild.iconURL({dynamic:true}))
			.setDescription(`[View Chat Online](${createdChat.url})`)
			.addField("Channel", message.channel.toString(), true)
			.addField("Chat Code", createdChat.ID, true)
		message.reply({embeds: [embed]});
	}
});

client.login("TOKEN")
```

## Contributing

© Chat Logs, 2021 - 2022 | TARIQ (contact@itariq.dev)
