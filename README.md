# Hack Ton Destin Bot

Bot Telegram qui envoie automatiquement un ebook PDF aux utilisateurs.

## Description

Ce bot permet d'envoyer un ebook PDF à toute personne qui interagit avec lui.  
Développé avec Python et la librairie `python-telegram-bot`.  

## Installation

1. Cloner ce dépôt  
2. Installer les dépendances :  
```bash

pip install -r requirements.txt
python bot.
python-telegram-bot==20.3
python-dotenv
import os
from dotenv import load_dotenv
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes

# Charger les variables d'environnement
load_dotenv()
TOKEN = os.getenv("BOT_TOKEN")

# Fonction déclenchée quand l'utilisateur tape /start
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("Bienvenue ! Voici ton ebook 📘")

    # Envoyer le fichier PDF
    with open("ebook.pdf", "rb") as pdf_file:
        await update.message.reply_document(pdf_file)

# Créer l'application et l'exécuter
if __name__ == '__main__':
    app = ApplicationBuilder().token(TOKEN).build()

    app.add_handler(CommandHandler("start", start))

    print("Bot démarré...")
    app.run_polling()
BOT_TOKEN=8235020028:AAGP7T4rzurbAuDtrzXR7jIX7A1S18RkjNc
