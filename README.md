<a:moneypack100:1179611532120821810> ** ดักอังเป่า**
```javascript
require('dotenv').config();
const { Client } = require('discord.js-selfbot-v13');
const { Webhook, MessageBuilder } = require('minimal-discord-webhook-node');
const twvoucher = require('@fortune-inc/tw-voucher');
const client = new Client({
  checkUpdate: false
});

// Config
const token = "MTAyNDE3MzAwODA5MDMwODY0MQ.GOBoo9.flKj-rqMrHhGmKq1Fb84OkjBHu1QEbG8XT5cbc"  // โทเค่นตัวเอง
const phone = "0942091264" //เบอร์
const url = "https://discordapp.com/api/webhooks/1161673071091011656/uDEO43HyEoca5jeINrRurrFvnrTFUScz_oIlsZ-7QrctxHO1IPgJCMNsbjEpgybEFve0" //webhook

client.on('ready', async () => {
    console.log(" ");
    console.log(`[✅]${client.user.username} Online !`);
    console.log(" ");
})

client.on('messageCreate', async (message) => {
  const fullLink = 'https://gift.truemoney.com/campaign/?';
  if (message.content.includes(fullLink)) {
    const voucherCodeStartIndex = message.content.indexOf(fullLink) + fullLink.length;

    // Extract the substring before the space (if any)
    let spaceIndex = message.content.indexOf(' ', voucherCodeStartIndex);
    if (spaceIndex === -1) {
      spaceIndex = message.content.length; // If no space is found, use the entire string
    }

    const voucherCode = message.content.slice(voucherCodeStartIndex, spaceIndex);
    const redeemlink = `${fullLink}${voucherCode}`;

    try {
      const redeemed = await twvoucher(`${phone}`, voucherCode);
      const hook = new Webhook(`${url}`);
      const embed = new MessageBuilder()
        .setTitle(`**Collect AungPao ( Success ) - เบอร์: ${phone}**`)
        .setDescription('_ _')
        .addField('- ผล', '_ _\n`✅`: ดักสำเร็จ !\n_ _\n_ _')
        .addField('- ลิ้งค์ซอง', `${fullLink}${voucherCode}\n_ _\n_ _`)
        .addField('- ชื่อเจ้าของซอง', `_ _\n${redeemed.owner_full_name}\n_ _\n_ _`)
        .addField('- จำนวนเงิน', `_ _\n${redeemed.amount}\n_ _\n_ _`)
        .setColor('#ffffff')
        .setImage('https://media.discordapp.net/attachments/1183701346420015106/1191391429021413407/wa.gif?ex=65a544bb&is=6592cfbb&hm=dbedf38ec411fd4a165a05489dbc3dd4e6692e02b128898a5ee23177fb01db77&=')
        .setThumbnail('https://media.discordapp.net/attachments/1190633389477351514/1191380448488730674/woah.gif?ex=65a53a81&is=6592c581&hm=49b5624636145958e031646e8ed6910f8fda911f9b14a6c7ea08126f432ff23a&=')
        .setFooter('Fake Link Club Aungpou', 'https://media.discordapp.net/attachments/1190633389477351514/1191379907251535932/woah.gif?ex=65a53a00&is=6592c500&hm=6c139b62b3b74f8ec4287392f49b6605e5199da16a37496271b53d790778d3e3&=')
        .setTimestamp();
      hook.send(embed)
      console.log(" ");
      console.log(`redeem ซอง ${redeemed.code} ของ ${redeemed.owner_full_name} จำนวน ${redeemed.amount} บาทแล้ว`);
      console.log(" ");
    } catch (err) {
      const hook_f = new Webhook(`${url}`);
      const embed_f = new MessageBuilder()
        .setTitle(`**Collect AungPao ( Failed ) - เบอร์: ${phone}**`)
        .setDescription('_ _')
        .addField('- ผล', '_ _\n`❌`: ดักไม่สำเร็จ\n_ _\n_ _')
        .addField('- ลิ้งค์ซอง', `${fullLink}${voucherCode}\n_ _\n_ _`)
        .setColor('#ffffff')
        .setImage('https://media.discordapp.net/attachments/1183701346420015106/1191391429021413407/wa.gif?ex=65a544bb&is=6592cfbb&hm=dbedf38ec411fd4a165a05489dbc3dd4e6692e02b128898a5ee23177fb01db77&=')
        .setThumbnail('https://media.discordapp.net/attachments/1190633389477351514/1191380448488730674/woah.gif?ex=65a53a81&is=6592c581&hm=49b5624636145958e031646e8ed6910f8fda911f9b14a6c7ea08126f432ff23a&=')
        .setFooter('Fake Link Club Aungpou', 'https://media.discordapp.net/attachments/1190633389477351514/1191379907251535932/woah.gif?ex=65a53a00&is=6592c500&hm=6c139b62b3b74f8ec4287392f49b6605e5199da16a37496271b53d790778d3e3&=')
        .setTimestamp();
      hook_f.send(embed_f);
      console.log(" ");
      console.error('FAILED');
      console.log(" ");
    }
  }
})

client.login(`${token}`);
```
