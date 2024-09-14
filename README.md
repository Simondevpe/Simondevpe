// server.js

// Load environment variables from .env
require('dotenv').config();

// Import the discord.js module
const { Client, GatewayIntentBits } = require('discord.js');

// Create a new Discord client instance
const client = new Client({
  intents: [
    GatewayIntentBits.Guilds,
    GatewayIntentBits.GuildMessages,
    GatewayIntentBits.MessageContent,
  ]
});

// When the bot is ready
client.once('ready', () => {
  console.log('Bot is online and ready!');
});

// When a message is sent in a channel
client.on('messageCreate', (message) => {
  // Ignore messages from the bot itself
  if (message.author.bot) return;

  // Respond to "hi"
  if (message.content.toLowerCase() === 'hi') {
    message.channel.send(`
      **What package do you want to buy? Here is what Simon offers:**

      **Simon Plus:**
      - Unrigger
      - Prediction
      - 3 algorithms for each game
      - ESP
      - **Price**: 400 weekly, 700 monthly, 1450 lifetime

      **Plus+ (Recommended):**
      - 30 algorithms (5-7 for each game)
      - We have a bot as well
      - Same as Plus but better
      - **Price**: 850 weekly, 1475 monthly, 2000 lifetime paid

      **Paid:**
      - 15 algorithms for each game
      - Best Unrigger with 6 methods
      - Best ESP
      - Best UI
      - Best Predictor
      - **This package is better than** 3vil, Mystic, Star, Thunder, and many others.
      - The only predictor that is better is LunarR.
      - Includes machine learning and AI player
      - **Price**: Custom pricing

      **Paid+:**
      - 100 algorithms in total
      - Powerful machine learning, AI algorithms, and AI player
      - Best AI algorithm and powerful machine learning combined
      - We also offer a bot
      - **Price**: Custom pricing

      **Bot:**
      - Best bot right now
      - Machine learning and advanced algorithms
    `);
  } else if (['plus+', 'simon plus', 'paid', 'paid+', 'bot'].some((package) => message.content.toLowerCase().includes(package))) {
    message.channel.send("Great! Please open a ticket and we will reply as fast as we can.");
  }
});

// Log in to Discord with your bot token
client.login(process.env.DISCORD_BOT_TOKEN);
