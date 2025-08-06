Mise à jour bot.py# Hack Ton Destin Bot

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

# Charger les variables d'environnement depuis le fichier .env
load_dotenv()
TOKEN = os.getenv("BOT_TOKEN")

# Fonction qui répond à la commande /start
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("Bienvenue ! Voici ton ebook 📘")

    # Envoyer le fichier PDF
    try:
        with open("ebook.pdf", "rb") as pdf_file:
            await update.message.reply_document(pdf_file)
    except FileNotFoundError:
        await update.message.reply_text("Erreur : le fichier ebook.pdf est introuvable.")

# Initialiser et lancer le bot
if __name__ == '__main__':
    if not TOKEN:
        print("Erreur : le token Telegram est manquant. Vérifie le fichier .env ou les variables Render.")
    else:
        app = ApplicationBuilder().token(TOKEN).build()
        app.add_handler(CommandHandler("start", start))
        print("Bot démarré...")
        app.run_polling()
