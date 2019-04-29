const ayarlar = require('../ayarlar.json');
const db = require('quick.db');

module.exports = async message => {
  
  let client = message.client;
  let prefix = await db.fetch(`prefix_${message.guild.id}`) || ayarlar.prefix
  if (message.author.bot) return;
  if (!message.content.startsWith(prefix)) return;
  let command = message.content.split(' ')[0].slice(prefix.length)
  let params = message.content.split(' ').slice(1)
  let perms = client.elevation(message);
  let cmd;
  if (client.commands.has(command)) cmd = client.commands.get(command);
  else if (client.aliases.has(command)) cmd = client.commands.get(client.aliases.get(command));
  
  let kanal = await db.fetch(`botuncalismamakanali_${message.channel.id}`)
  if (kanal == null) {
  if (cmd) {
    if (perms < cmd.conf.permLevel) return;
    cmd.run(client, message, params, perms);
  }
  }
  
  if (kanal == 'calismiyor') {
    if (cmd.help.name == `çalışmakanal`) {
    cmd.run(client, message, params, perms)
    return;
  }
    if (cmd) return;
  }
};