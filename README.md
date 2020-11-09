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
    
    public void save() { try { config.save(file); } catch(Exception e) { e.printStackTrace(); } }

    public File getFile() { return file; }
    public YamlConfiguration getConfig() { return config; }
}
```
