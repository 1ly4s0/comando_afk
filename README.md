![Node build](https://github.com/eritislami/evobot/actions/workflows/node.yml/badge.svg)

![logo](https://cdn.discordapp.com/attachments/933698201486237716/947555143795228682/Diseno_sin_titulo_22.png)

# 🤖 Tutorial Discord Bot (TECNO BROS)
> Código del bot del tutorial de TECNO BROS, el vídeo es [este](https://youtu.be/5Rn375Uzh4c)
## Requisitos

1. Tener un bot de Discord creado **[Guía](https://www.youtube.com/watch?v=qXev2kf-q_0)**
2. Tener Discord.js V12 o Discord.js V13 **[Guía](https://www.youtube.com/watch?v=qXev2kf-q_0)**
3. Tener el bot hosteado o en tu PC **[Guía](https://www.youtube.com/watch?v=0MkVTtLoMiI)**  
4.1 **(Opcional)** Tener el bot en algun host **[Guía](https://www.youtube.com/watch?v=0MkVTtLoMiI)**

## 🚀 Código de AFK

```js
const Discord = require("discord.js");
const { MessageEmbed } = require("discord.js");

const db = require("quick.db");

const client = new Discord.Client({
    intents: 3276799
});

client.on("ready", () => {
    console.log(`✅ ¡Logueado como ${client.user.tag}!`);
});

client.on("messageCreate", async message => {
    if(!db.has(`${message.author.id}-afk`)) return;

    let razon = await db.get(`${message.author.id}-afk`);
   
    message.channel.send(`${message.author.tag} ahora no estás AFK porque has vuelto, la razón era: ${razon}`);
    db.delete(`${message.author.id}-afk`);
})

client.on("messageCreate", async message => {
    if(message.content.startsWith("tb!afk")) {
    const args = message.content.trim().split(/ +/g);

    let razon = args.slice(1).join(" ");
    if(!razon) {
        razon = "No especificado";
    }
    const embed = new MessageEmbed()
    .setTitle("AFK")
    .setDescription(`${message.author.tag} ahora estás AFK por ${razon}`)
    .setThumbnail(message.author.displayAvatarURL());

    await db.set(`${message.author.id}-afk`, razon);

    return message.channel.send({ embeds: [embed]});
    }
})

client.on("messageCreate", async message => {
    let mencionado = message.mentions.members.first();
    if(!mencionado) return;
    if(db.has(`${mencionado.id}-afk`)) {
        let razon = await db.get(`${mencionado.id}-afk`);
        message.channel.send(`${mencionado.user.tag} está AFK por ${razon}`);
    }
})






```
Después de modificar o añadir algo al código, recuerda o reiniciar tu bot o usar el comando `node index.js` para que los cambios se apliquen.

## ⚙️ Uso:

## AFK
![logo](https://cdn.discordapp.com/attachments/933698201486237716/1014627380070981632/unknown.png)




## 📝 Créditos
* [DISCORD](https://discord.gg/tecnobros)
* [YOUTUBE](https://youtube.com/tecnobros)

Copyright © **1ly4s0#2477** - 2022
