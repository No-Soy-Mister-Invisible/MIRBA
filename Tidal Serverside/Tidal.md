# **Tidal Serverside Analysis**

---

## **1. Backdoor Discovery**

I was bored, so I decided to scan some Roblox assets using my trusty Invis Model Scanner, a tool I created to scan models for interesting surprises. To my "surprise", I came across yet another infected module that novice developers could download without checking. So, being curious, I decided to play around with the ss.

After analyzing it, I unraveled its entire functionality. And here’s the interesting part.

---

## **2. The Injector**

The exploit uses a free injector with no obfuscation at all.

🔗 **Injector Download:** [Tidal Injector.rbxm](https://biteblob.com/Information/tlZyi5yr1GFajm/Tidal%20Injector.rbxm)

If you have basic Lua knowledge, you can literally turn this injector and its GUI into your plaything. They didn't even try to secure it, so reversing its functionality was ridiculously easy. Just tearing it apart revealed the entire structure of how it interacts with the infected server.

---

## **3. The Loader**

The malware starts its process with a low-quality but obfuscated loader that loads and executes malicious scripts on the infected server.

🆔 **17858917701**

🔗 **Loader Download:** [Tidal Loader.rbxm](https://biteblob.com/Information/PIOwwbyb0Lhvbu/Tidal%20Loader.rbxm)

Originally, this file was over 90 MB because they attempted to use a useless "crash method," which I’m removing. In fact, I left this note in the loader:

```lua
-- 💀 Bro really thinks the "crash" method really works
-- Original ID: 17858917701
```

I don't know what's worse, the idea that this would work or that someone thought it was a good security strategy.

---

## **4. The GUI**

The exploit includes a graphical interface that allows attackers to control the infected server. Some parts of this GUI were also obfuscated, but that didn't help much.

🆔 **86572829119745**

🔗 **GUI Download:** [Tidal GUI.rbxm](https://biteblob.com/Information/6iohxukt5AiUfx/Tidal%20GUI.rbxm)

From this GUI, operators can execute remote commands, manage users, and modify the server environment without the original owner having the slightest clue about what’s happening.

I also left this note in the GUI:

```lua
-- 💀 Bro really thinks the "crash" method really works
-- Original ID: 86572829119745
```

---

## **5. Malware active**

This malware disguises itself as a "legitimate" asset in the Toolbox, infecting games whose developers install it without reviewing the code. Once inside, it opens a remote connection that gives full server access to the serverside operators. The backdoor is called Tidal Serverside, and their community can be found on their Discord server:

🔗 [Tidal Serverside - Discord](https://discord.gg/adfEG4zM6S)

---

## **6. Send information**

Every time the infected server starts, the script begins sending information to an external API. The collected data includes:

- **HttpService**
- **Players** (List of players on the server)
- **RunService** (Game state)
- **PlaceId** (Infected game identifier)
- **GameId** (Global game ID)
- **JobId** (Running server identifier)
- **PlaceVersion** (Game version)

All this information is sent to the following API:

🔗 `https://sentinell.vercel.app/v1/logs`

This was just a quick review, and I didn’t pay much attention to it because, at this point, it was obvious this was just another Roblox malware asset.

---

## **7. Serverside Structure and Access Verification**

The exploit operators use the following API to check if a user is whitelisted and has permission to execute commands:

🔗 `https://roproxify.vercel.app/v2/analytics/(user ID)`

To ensure that only "authorized" people can execute commands on infected servers, the backdoor creators implemented a script verification system:

🔗 `https://sentinell.vercel.app/v2/script`

This supposedly provides security, but in practice, it’s a joke. Its implementation is so pathetic that anyone with minimal Lua knowledge can bypass it effortlessly.

---

## **8. Conclusion**

This backdoor is available in the public Roblox Toolbox, meaning that any unsuspecting developer who installs it is unknowingly handing their server over to attackers. The solution is simple: review every asset before using it. If you already have this in your game, remove it immediately.

If Roblox took these issues seriously, they would have blocked these APIs by now, but here we are.

---

Mr Invisible out.