# SpigotConfigAPI

This is a Spigot Configuration API made by me, it's extremely useful & easy to use.


**How to use**\
Copy and paste the code at the bottom of the page, into a new class called something like 'Config'. Then in your main spigot class that extends JavaPlugin, create a variable like this above your onEnable();
```java
private Config motdConfig;
```
In your onEnable() initialize the config by doing
```java
motdConfig = new Config("motd.yml", this);
```
After adding those methods into your code, you need to make the actual 'config.yml' or whatever your confiuration is called. You can then access the configuration file, and get coding using configurations in Spigot.

**Actual code - put in Config.class**
```java
public class Config {
    private final File file;
    private final YamlConfiguration config;

    public Config(String name, Plugin plugin) {
        file = new File(plugin.getDataFolder(), name);

        if(!file.exists()) {
            file.getParentFile().mkdir();
            plugin.saveResource(name, true);
        }

        config = new YamlConfiguration();
        try { config.load(file); } catch(Exception e) { e.printStackTrace(); }
    }
    public void save() {
        try {
            config.save(file);
        } catch(Exception e) {
            e.printStackTrace();
        }
    }
    public String getColoredString(String path) {
        return ChatColor.translateAlternateColorCodes('&', config.getString(path));
    }

    public void setLocation(Location loc, String place) {
        config.set(place + ".WORLD", loc.getWorld().getName());
        config.set(place + ".X", loc.getX());
        config.set(place + ".Y", loc.getY());
        config.set(place + ".Z", loc.getZ());
        config.set(place + ".YAW", loc.getYaw());
        config.set(place + ".PITCH", loc.getPitch());
        save();
    }

    public Location getLocation(String place) {
        return new Location(Bukkit.getWorld(config.getString(place + ".WORLD")), config.getDouble(place + ".X"), config.getDouble(place + ".Y"), config.getDouble(place + ".Z"), config.getLong(place + ".YAW"), config.getLong(place + ".PITCH"));
    }

    @SuppressWarnings("unchecked")
    public ItemStack[] getItemArray(String path) {
        return ((List<ItemStack>) config.get(path)).toArray(new ItemStack[0]);
    }

    public File getFile() { return file; }
    public YamlConfiguration getConfig() { return config; }
}
```
