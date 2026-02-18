# Tehran Poker - Server Configuration

This repository contains the automatic server configuration for Tehran Poker clients.

## 🎯 Purpose

Allows you to update the server URL for all clients without rebuilding or redistributing the application. Clients automatically fetch the latest server configuration from this GitHub repository.

## 📋 Configuration File

**`server-config.json`** - Main configuration file

```json
{
  "version": "1.0.1",
  "server_url": "https://play.tpoker.com",
  "backup_servers": [
    "http://localhost:5001",
    "https://api.tpoker.com"
  ],
  "last_updated": "2026-02-18T11:50:00Z",
  "features": {
    "auto_update": true,
    "fallback_enabled": true,
    "health_check_interval": 60
  }
}
```

## 🔄 How It Works

1. **Client Startup**: GUI fetches `server-config.json` from GitHub
2. **Auto-Sync**: Uses `server_url` field as primary server
3. **Local Cache**: Saves config locally for offline use
4. **Fallback**: If GitHub unavailable, uses cached config or localhost

## 📝 Updating Server URL

To change the server URL for all clients:

1. Edit `server-config.json`
2. Update `server_url` field
3. Update `last_updated` timestamp
4. Commit and push to GitHub
5. Clients will auto-sync on next launch

```bash
# Example workflow
nano server-config.json
# Change server_url to new address
git add server-config.json
git commit -m "Update server URL to new-server.com"
git push origin main
```

## 🌐 GitHub Raw URL

Clients fetch from:
```
https://raw.githubusercontent.com/tehranpoker/server/main/server-config.json
```

## 🔒 Private Repository

This repository can be private. Clients use raw.githubusercontent.com which works with private repos if you have access token (or public for easier deployment).

## 🛡️ Security Features

- **HTTPS Only**: Production servers should use HTTPS
- **Version Tracking**: Track config versions for rollback
- **Cache System**: Local cache prevents downtime if GitHub unavailable
- **Fallback Chain**: GitHub → Cache → Localhost

## 📊 Fields Reference

| Field | Type | Description |
|-------|------|-------------|
| `version` | string | Config version for tracking |
| `server_url` | string | Primary server URL (auto-synced) |
| `backup_servers` | array | Fallback servers (future use) |
| `last_updated` | string | ISO timestamp of last update |
| `features.auto_update` | boolean | Enable auto-update (future) |
| `features.fallback_enabled` | boolean | Enable fallback servers |
| `features.health_check_interval` | number | Seconds between checks |

## 🚀 Client Behavior

### On First Launch:
1. Fetch from GitHub → Success: Use GitHub URL
2. GitHub fails → Use localhost:5001

### On Subsequent Launches:
1. Fetch from GitHub → Success: Update cache, use new URL
2. GitHub fails → Use cached config
3. Cache fails → Use localhost:5001

## 💡 Best Practices

1. **Always update `last_updated`** when changing config
2. **Test server URL** before committing
3. **Keep backup_servers updated** for redundancy
4. **Use semantic versioning** for config versions
5. **Document changes** in commit messages

## 📞 Support

For issues or questions, contact Tehran Poker development team.