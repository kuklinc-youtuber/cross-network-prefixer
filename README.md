# 🌐 CrossNetworkPrefixer

[![Available on Modrinth](https://img.shields.io/badge/Available_on-Modrinth-00AF5C?style=for-the-badge&logo=modrinth)](https://modrinth.com/plugin/cross-network-prefixer)

![Built with Java 21](https://raw.githubusercontent.com/intergrav/devins-badges/refs/heads/v3/assets/cozy/built-with/java21_vector.svg)
![Supported Spigot](https://raw.githubusercontent.com/intergrav/devins-badges/refs/heads/v3/assets/cozy/supported/spigot_vector.svg)
![Supported Paper](https://raw.githubusercontent.com/intergrav/devins-badges/refs/heads/v3/assets/cozy/supported/paper_vector.svg)
![Available on Modrinth](https://raw.githubusercontent.com/intergrav/devins-badges/refs/heads/v3/assets/cozy/available/modrinth_vector.svg)

A powerful, high-performance Spigot plugin designed for multi-proxy networks and partnered Minecraft servers. CrossNetworkPrefixer allows you to dynamically alter player prefixes and TAB-list sorting weights based on **who is looking at whom**. Perfect for server networks that share chat or TAB lists across different proxy clusters (via Velocity or BungeeCord) but want to maintain clear, localized staff hierarchy and visibility.

---

## ✨ Features (Release v1.0)

### 👀 Viewer-Dependent Context
Display completely different prefixes and sorting weights depending on the viewing player's origin network.

### 📋 Smart Hierarchy Sorting
Dynamically adjust TAB weights to ensure local staff members are always sorted at the very top of their respective network's TAB list.

### 🔗 LuckPerms Meta Integration
Seamlessly integrates with the LuckPerms Meta-Data API to instantly determine a player's origin network and real group inheritance.

### 🧩 PlaceholderAPI & Relational Support
Fully implements standard and relational placeholders for complete compatibility with advanced TAB and Chat formatters.

### 🛡️ OP Status Bypass Protection
Evaluates group inheritance directly from LuckPerms API layers, preventing standard Minecraft Operator (`/op`) permissions from breaking group sorting order.

---

## 🔧 Placeholders

The plugin registers the `crossnetworkprefixer` identifier.

| Placeholder | Description |
|------------|-------------|
| `%crossnetworkprefixer_prefix%` | Returns the formatted prefix for the player themselves. |
| `%crossnetworkprefixer_weight%` | Returns the weight value for sorting. |
| `%rel_crossnetworkprefixer_prefix%` | **Recommended for TAB/Chat**. Shows the target's prefix adjusted to the viewer's network profile. |
| `%rel_crossnetworkprefixer_weight%` | Relational sorting weight based on the viewer's network profile. |

---

## ⚙️ Configuration

<details>
<summary><strong>Click to view example config.yml</strong></summary>

```yaml
# =========================================================================
#                 CROSSNETWORKPREFIXER CONFIGURATION
# =========================================================================

# The LuckPerms meta-key used to identify which network/server the player is from.
# Example: If a player has the meta "from=network_one", the plugin loads that profile.
meta-key: "from"

# Default network profile used if a player doesn't have the meta key
# or if their network profile is not defined below.
# Set to "none" to completely disable prefixes for unknown networks.
fallback-network: "none"

# =========================================================================
# Network Profiles (Configure your networks here)
# =========================================================================
networks:

  # -------------------------------------------------------------------------
  # EXAMPLE PROFILE A: network_one
  # -------------------------------------------------------------------------
  network_one:
    priority:
      - "admin_network_one"
      - "mod_network_one"
      - "admin_network_two"
      - "vip"
      - "default"

    admin_network_one:
      prefix: "&4&lADMIN &8» &c"
      weight: "1000"

    mod_network_one:
      prefix: "&c&lMOD &8» &c"
      weight: "900"

    admin_network_two:
      prefix: "&d&lPARTNER &8» &d"
      weight: "500"

    vip:
      prefix: "&a&lVIP &r"
      weight: "100"

    default:
      prefix: "&7"
      weight: "1"

  # -------------------------------------------------------------------------
  # EXAMPLE PROFILE B: network_two
  # -------------------------------------------------------------------------
  network_two:
    priority:
      - "admin_network_two"
      - "admin_network_one"
      - "vip"
      - "default"

    admin_network_two:
      prefix: "&2&lADMIN &8» &a"
      weight: "1000"

    admin_network_one:
      prefix: "&5&lPARTNER &8» &d"
      weight: "500"

    vip:
      prefix: "&a&lVIP &r"
      weight: "100"

    default:
      prefix: "&7"
      weight: "1"
```

</details>

---

## 🌍 Real-World Example

Let's assume **Admin One** controls **Network One** and **Admin Two** controls **Network Two**.

With a normal chat plugin, both players might simply appear as:

```text
[ADMIN] Admin One
[ADMIN] Admin Two
```

This provides no distinction between local and partner staff.

### When a player from Network One opens the TAB list

- Admin One appears as **&4&lADMIN**
- Weight: **1000**
- Sorted at the very top

- Admin Two appears as **&d&lPARTNER**
- Weight: **500**
- Sorted below local staff

### When a player from Network Two opens the TAB list

- Admin Two appears as **&2&lADMIN**
- Weight: **1000**
- Sorted at the very top

- Admin One appears as **&5&lPARTNER**
- Weight: **500**
- Sorted below local staff

This ensures staff members maintain localized ranking authority and prominent visibility on their home instances while partner-network staff are clearly identified as guests.

---

## ⚡ Why Use CrossNetworkPrefixer?

✅ Perfect for partnered Minecraft networks

✅ Lightweight and optimized

✅ No external database required

✅ LuckPerms-powered architecture

✅ Viewer-dependent prefixes

✅ Viewer-dependent TAB sorting

✅ PlaceholderAPI compatible

✅ Supports complex network structures

---

## 📥 Installation

1. Download the latest release.
2. Place the JAR into your server's `plugins/` folder.
3. Restart the server.
4. Configure `config.yml`.
5. Set up your LuckPerms meta values.
6. Use the placeholders in TAB, chat plugins, scoreboards, or wherever needed.

---

## 🛠️ Support & Development

CrossNetworkPrefixer is actively maintained and optimized.

Feature suggestions, bug reports, and contributions are always welcome.

Thank you for using **CrossNetworkPrefixer** ❤️
