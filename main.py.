import discord
from discord.ext import commands
import requests
import os

# These pull your links from the "Environment Variables" we will set up in Render
TOKEN = os.environ.get('TOKEN')
DB_URL = os.environ.get('DATABASE_URL')

# Basic setup for the bot
intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix="!", intents=intents)

@bot.event
async def on_ready():
    print(f"✅ Bot is online as {bot.user}")

# The command you will type in Discord
@bot.command()
async def farm(ctx, state: str):
    state = state.lower()
    if state in ["on", "off"]:
        # This sends "true" for on and "false" for off to your Firebase link
        is_on = (state == "on")
        # We add "/data.json" to the end of your link so Firebase accepts it
        requests.patch(f"{DB_URL}/data.json", json={"autoFarm": is_on})
        await ctx.send(f"🚜 Auto-farm has been turned: **{state.upper()}**")
    else:
        await ctx.send("❌ Please use `!farm on` or `!farm off`")

bot.run(TOKEN)
