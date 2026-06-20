# Telegram Mini Parcel App

A Next.js Telegram Mini App for parcel booking.

## Features
- Mobile-first booking form
- Required sender/receiver/parcel fields
- Product category selection
- Confirmation page and printable receipt
- Sends booking notification to Telegram group
- Admin order list
- CSV export
- Supabase-ready, with local JSON fallback for development

## Setup

```bash
npm install
cp .env.example .env.local
npm run dev
```

Open `http://localhost:3000`.

## Telegram setup
1. Create bot in BotFather using `/newbot`.
2. Copy token into `BOT_TOKEN`.
3. Add bot to your Telegram group.
4. Get group chat id and put it in `TELEGRAM_GROUP_CHAT_ID`.
5. Deploy to Vercel.
6. In BotFather: `/mybots` → your bot → Bot Settings → Menu Button → Web App → add your HTTPS URL.

## Supabase table
Create table `orders`:

```sql
create table orders (
  id text primary key,
  created_at timestamptz default now(),
  sender_name text not null,
  sender_phone text not null,
  receiver_name text not null,
  receiver_phone text not null,
  origin text not null,
  destination text not null,
  weight_kg numeric not null,
  length_cm numeric not null,
  width_cm numeric not null,
  height_cm numeric not null,
  product_type text not null,
  package_count integer not null,
  remark text,
  status text default 'Pending Drop-off'
);
```

Use a service role key only on the server, never expose it in frontend code.
