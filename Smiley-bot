import discord
from discord.ext import commands
import random

class MyClient(discord.Client):
    async def on_ready(self):
        print('Logged on as {0}!'.format(self.user))

bot = commands.Bot(command_prefix='Smiley, ')

bot.remove_command('help')

@bot.command()
async def hello(ctx):
    await ctx.send('Hello')


@bot.event
async def on_ready():
    print('Logged in as')
    print(bot.user.name)
    print(bot.user.id)
    print(bot.latency)
    print("Smiley Bot Commands :D")
    print('------')

@bot.command()
async def purge(ctx,*,Num=0):
    Num += 1
    await ctx.channel.purge(limit=Num)
    Num -= 1
    Purge = discord.Embed(title='Purge', description=f'{Num} messages has successfully been purged.',colour=discord.Color(0x15A636))
    await ctx.send(embed=Purge)

@bot.command()
async def note(ctx, a: str):
    a = a.replace("_", " ")
    print(a)
    await ctx.send(f'The note, "{a}", has been added to the console.')

@bot.command()
async def ping(ctx):
    await ctx.send(f"Pong! {bot.latency}")

@bot.command()
async def help(ctx):
    help = discord.Embed(title='Help!', description='''Basic commands for everyone: \n--ping\n--hello\n--note (Do not abuse it!)
    Commands for moderation:\n--purge\n--mute\n--clearmsgs (on hold)\n--ban 
    Random Commands:
    --new_file\nCreates a new file\n--load_file\nLoads a file (I\'ll work on a way to allow you to see files)''', colour=discord.Color(0x15A636))
    await ctx.send(embed=help)

@bot.command()
async def mute(ctx, mes: str):
    mes = mes.replace('>', '')
    mes = mes.replace('<@!', '')
    mes = int(mes)
    print(f'Muted: {mes}')
    await ctx.send(f'Muted the user: <@{mes}>, id: {mes}')

@bot.command()
async def new_file(ctx, filename: str, *, data):
    newfile = open(f'{filename}.txt',"a+")
    newfile.write(str(data))
    newfile.close()

@bot.command()
async def load_file(ctx, filename: str):
    file = open(f'{filename}.txt', 'r+')
    data = file.read()
    await ctx.send(data)
    file.close

@bot.command()
async def addmoney(ctx, amount: str):
    fi = open('users.txt', 'r+')
    ficont = fi.read()
    if str(ctx.message.author.id) in ficont:
        fil = open(f'{ctx.message.author.id}.txt', 'r+')
        balance = fil.read()
        amount = int(amount)
        amount += int(balance)
        fil.seek(0)
        fil.truncate(0)
        fil.write(str(amount))
        fil.close()
        fi.close()
    else:
        fi = open('users.txt', 'w')
        fi.write(f'\n{ctx.message.author.id}')
        fil = open(f'{ctx.message.author.id}.txt', 'w')
        fil.write(str(amount))
        fil.close()
        fi.close()


bot.run('[token here]')
