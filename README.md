# ZRoleRestore
ZRoleRestore is a powerful and intuitive Discord cog designed to solve a common server management headache: members leaving and rejoining only to have lost all of their roles This cog automatically saves a users roles when they leave and seamlessly restores them upon their return ensuring community continuity and saving administrators valuable time
> 💡 **Built for the Zygnal Ecosystem — to download and use this extension, you must be part of the Zygnal Ecosystem.**  
> This extension (cog) is part of the **Zygnal Ecosystem** and is only available through its supported platforms.  
> You can use it with:  
> - The **[Discord Bot Framework](https://github.com/TheHolyOneZ/discord-bot-framework)** — ideal for developers who want full control and flexibility *(includes an integrated extension marketplace)*, or  
> - The **[ZygnalBot](https://zygnalbot.de)** — a prebuilt, plug-and-play Discord bot *(also includes an integrated extension marketplace)*.  
>
> Browse and install extensions at [zygnalbot.com/extension](https://zygnalbot.com/extension).  
> For help or community discussions, join us on Discord: [discord.gg/sgZnXca5ts](https://discord.gg/sgZnXca5ts)
# ZRoleRestore Bot Cog

ZRoleRestore is a powerful and intuitive Discord cog designed to solve a common server management headache: members leaving and rejoining, only to have lost all of their roles. This cog automatically saves a user's roles when they leave and seamlessly restores them upon their return, ensuring community continuity and saving administrators valuable time.

---

## 📋 Table of Contents

* [Why ZRoleRestore?](#-why-zrolerestore)
* [Key Features](#-key-features)
* [How It Works](#-how-it-works)
* [Getting Started](#-getting-started)
* [Commands](#-commands)
* [The Control Panel: A Deep Dive](#-the-control-panel-a-deep-dive)
* [Frequently Asked Questions (FAQ)](#-frequently-asked-questions-faq)

---

## 🤔 Why ZRoleRestore?

Managing a Discord server involves keeping track of member roles, which can signify status, access, or achievements. When a member leaves and comes back, manually re-assigning dozens of roles is tedious and prone to error. ZRoleRestore automates this entire process.

* **Save Time:** No more scrolling through audit logs or asking members what roles they had.
* **Maintain Consistency:** Ensure that returning members get their exact roles back, preserving their place in the community.
* **Empower Admins:** A simple, powerful control panel puts all the configuration at your fingertips without needing to edit code or use complex commands.

---

## ✨ Key Features

* **🔄 Automatic Save & Restore**: The core of the cog. It silently logs roles when a member leaves and automatically restores them if they rejoin.
* **🔒 Local & Secure Database**: All data is stored in a local SQLite database file (`zrolerestore.db`) within your bot's data folder. You maintain full control and privacy over your server's data.
* **🔧 All-in-One Control Panel**: A beautiful and interactive UI allows you to manage every single setting with the click of a button.
* **🗑️ Automatic Data Pruning**: Set a retention period (e.g., 180 days) to automatically delete old role data, keeping your database clean and respecting user privacy.
* **🎯 Granular Role Filtering**: You can specify *only* the roles you want to save. This is perfect for ignoring temporary or cosmetic roles and only saving important ones like "Moderator" or "VIP".
* **➕ Automatic Role Assignment**: Designate specific roles to be added to *every* joining member, which is great for verification or default roles, in addition to their restored ones.
* **🔨 Smart Ban Handling**: Optionally, you can configure the cog to automatically delete a user's saved data when they are banned, preventing them from getting privileged roles back upon a potential return.
* **📊 Data Export**: Generate a complete JSON export of all saved role data for your server with a single click, perfect for backups or analysis.

---

## ⚙️ How It Works

The process is simple and happens entirely in the background once enabled:

1.  **A Member Leaves**: The bot detects the `on_member_remove` event.
2.  **Roles are Saved**: If the system is enabled for your server, the bot records the member's role IDs into the local SQLite database, along with a timestamp. It respects any "Filter Roles" you've set.
3.  **A Member Rejoins**: The bot detects the `on_member_join` event.
4.  **Roles are Restored**: The bot looks up the member's ID in the database. If a record is found (and hasn't expired due to the auto-delete setting), it re-applies the saved roles. It will also apply any "Add Roles" you've configured.

---

## 🚀 Getting Started

### Installation

1.  Place the `ZRoleRestore.py` file in your bot's `cogs` directory.
2.  Load the cog through your bot's standard loading command (e.g., `[p]load zrolerestore`).

### First-Time Setup

1.  Use the `/zrolerestore` or `[p]zrolerestore` command to open the control panel.
2.  Click the **"Toggle Role Restore"** button. The status light in the embed should turn green, indicating the system is now active.
3.  (Recommended) Click **"Set Auto-Delete Days"** and set a reasonable number (e.g., `180`) to manage your data automatically.
4.  Configure any other settings as needed. That's it!

---

## 💻 Commands

Accessing the control panel is simple. All commands require **Administrator Permissions**.

* **Slash Command**: `/zrolerestore`
* **Prefix Command**: `[p]zrolerestore` (Alias: `[p]zrr`)

*Note: Only one control panel can be active per server at a time. The panel expires and disables itself after 10 minutes of inactivity*.

---

## 🎛️ The Control Panel: A Deep Dive

This is the heart of the cog. Here is a detailed breakdown of each option.

### `🔄 Toggle Role Restore`
The main on/off switch. Green means it's active and saving/restoring roles. Gray means it is completely disabled.

### `⏰ Set Auto-Delete Days`
This opens a pop-up where you can define how long user data is stored after they leave. If a user is gone for longer than this period, their data is deleted. Set to `0` to store data indefinitely.

### `🔨 Toggle Ban Handling`
When enabled (green), if a user is banned from the server, their saved role data will be immediately deleted from the database. This is useful to ensure banned members don't automatically regain sensitive roles if they are unbanned and rejoin.

### `🎯 Set Filter Roles`
Allows you to create a whitelist of roles that the cog should save. If this list has any roles in it, **only** roles on this list will be saved. If the list is empty, all roles are saved. You will be prompted to provide a comma-separated list of role IDs.

### `➕ Set Add Roles`
Allows you to create a list of roles that will be given to *every* member who joins the server, in addition to any roles they get restored. This is perfect for auto-assigning a "Member" or "Verified" role.

### `📊 Export Role Data`
This will generate and send you a `.json` file containing all the user role data currently stored for your server. This is useful for creating backups or for manual inspection.

### `🗑️ Clear User Data`
> **⚠️ This is a destructive and irreversible action.**
This button permanently deletes all saved user role information for your server from the database.

### `⚠️ Clear Settings`
> **⚠️ This is a destructive and irreversible action.**
This button resets the cog's configuration for your server back to its default state (disabled, no auto-delete, etc.).

---

## ❓ Frequently Asked Questions (FAQ)

**Q: Where is my server's data stored?**
A: All data is stored locally in a file named `zrolerestore.db`, located in the `data/zrolerestore/` directory of your bot's instance. It is not shared with anyone.

**Q: What happens if a role that was saved is later deleted from the server?**
A: The bot is smart enough to handle this. When restoring, if it cannot find a role by its ID, it will simply skip it and continue applying the other valid roles.

**Q: Why did the control panel buttons stop working?**
A: For security and performance, the control panel automatically expires after 10 minutes. The buttons will become disabled, and you simply need to run the `/zrolerestore` command again to open a new one.

**Q: Can I use this for multiple servers?**
A: Yes! The cog is multi-guild compatible. All settings and user data are stored on a per-server (guild) basis.
