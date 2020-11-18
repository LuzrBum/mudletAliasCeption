# mudletAliasCeption
An alias for the [Mudlet](https://www.mudlet.org/) MUD client, written in LUA that allows creating a new alias by typing only (without having to click into the Mudlet "Alias" editor)

# Syntax
`alias <myNewAliasName> <the string to send to the MUD when user types myNewAliasName>`
  
# Bugs/Weaknesses
* Does not support parameters: `myNewAliasName MoreTextHere` will strip away MoreTextHere
* Does not do anything if alias already exists - because Mudlet permAlias() function creates duplicates by design, and there is no deleteAlias() function (?)

# Installation
See [alias.txt](/alias.txt) file or below
![Screenshot](/image.png)

```
-- HOW TO INSTALL IN MUDLET:
-- Create a new alias in Mudlet
-- Name = alias
-- Pattern = ^alias
-- Command =[blank]
-- Paste this code in the Lua box
-- Save and activate

local myCmd=command

-- Ignore first word in line ="alias" command sent to the client
local myCmdWithoutFirstWord=string.sub(myCmd, string.find(myCmd," ")+1)

-- Second word in line = my new alias/command
local secondWord = string.sub(myCmdWithoutFirstWord,0,string.find(myCmdWithoutFirstWord," ")-1)

-- Everything after the second  word = the string to be "send(t)" to MUD
local myCmdWithoutSecondWord=string.sub(myCmdWithoutFirstWord,string.find(myCmdWithoutFirstWord," ")+1)

-- oh man, "exists()" retourns a COUNT
if exists(secondWord, "alias")>0 then
  echo("Alias >>>"..secondWord.."<<< already exists, please edit in editor!!!")
end

if exists(secondWord, "alias")==0 then
  echo("Alias >>>"..secondWord.."<<< not found - creating  - Note: the new alias will be executed if creation is successful!")
  local myParameter = "send (\""..myCmdWithoutSecondWord.."\")"
  permAlias(secondWord,"",secondWord,myParameter)
end```
