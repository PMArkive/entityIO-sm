# Descriptions
Hook or get informations about entity inputs and outputs. Only tested in CS:GO.

# Dependencies
dhooks - https://forums.alliedmods.net/showpost.php?p=2588686&postcount=589

# Game Bugs
If you change map entities with Stripper (or other plugins based on OnLevelInit), then the paramType in EntityIO_OnEntityInput can be EntityIO_FieldType_String.

# Enums
```sourcepawn
enum EntityIO_FieldType
{
	EntityIO_FieldType_None,
	EntityIO_FieldType_Float,
	EntityIO_FieldType_String,
	EntityIO_FieldType_Vector,
	EntityIO_FieldType_Integer,
	EntityIO_FieldType_Boolean,
	EntityIO_FieldType_Character,
	EntityIO_FieldType_Color,
	EntityIO_FieldType_Entity
}
```

# Forwards
```sourcepawn
/**
 * Called when an entity receives an input.
 *
 * @param entity             Entity's index.
 * @param input              Input's name.
 * @param caller             Caller's index.
 * @param activator          Activator's index.
 * @param paramType          Parameter's type.
 * @param paramValue         Parameter's value.
 * @param paramArray         Parameter's value as an array.
 * @param paramString        Parameter's value as a string.
 * @param outputID           Output's ID.
 */
void EntityIO_OnEntityInput(int entity, const char[] input, int caller, int activator, EntityIO_FieldType paramType, any paramValue, const any[] paramArray, const char[] paramString, int outputId);
```

# Natives
## Inputs
```sourcepawn
/**
 * Retrieves the first input's address from an entity.
 *
 * @param entity         Entity's index.
 * @param dataMap        Datamap's address.
 * @param address        Input's address.
 * @error                Invalid entity index.
 * @return               True if an input was found, false otherwise.
 */
bool EntityIO_FindEntityFirstInput(int entity, Address& dataMap, Address& address);

/**
 * Retrieves the next input's address from an entity.
 *
 * @param dataMap        Datamap's address.
 * @param address        Input's address.
 * @error                Invalid datamap address, invalid address.
 * @return               True if an input was found, false otherwise.
 */
bool EntityIO_FindEntityNextInput(Address& dataMap, Address& address);

/**
 * Returns whether or not an input can be accepted by an entity.
 *
 * @param entity        Entity's index.
 * @param input         Input's name.
 * @error               Invalid entity index.
 * @return              True if the input can be accepted, false otherwise.
 */
bool EntityIO_HasEntityInput(int entity, const char[] input);

/**
 * Retrieves an input's name from an entity.
 *
 * @param address        Input's address.
 * @param input          Buffer to store the input's name.
 * @param maxLen         Maximum length of string buffer.
 * @error                Invalid address.
 * @return               Number of cells written.
 */
int EntityIO_GetEntityInputName(Address address, char[] input, int maxLen);
```

## Outputs
```sourcepawn
/**
 * Retrieves the first output's address from an entity.
 *
 * @param entity         Entity's index.
 * @param dataMap        Datamap's address.
 * @param address        Output's address.
 * @error                Invalid entity index.
 * @return               True if an output was found, false otherwise.
 */
bool EntityIO_FindEntityFirstOutput(int entity, Address& dataMap, Address& address);

/**
 * Retrieves the next output's address from an entity.
 *
 * @param dataMap        Datamap's address.
 * @param address        Output's address.
 * @error                Invalid datamap address, invalid address.
 * @return               True if an output was found, false otherwise.
 */
bool EntityIO_FindEntityNextOutput(Address& dataMap, Address& address);

/**
 * Retrieves an output's offset.
 *
 * @param entity        Entity's index.
 * @param output        Output's name.
 * @error               Invalid entity index.
 * @return              Output's offset, -1 on failure.
 */
int EntityIO_FindEntityOutputOffset(int entity, const char[] output);

/**
 * Returns whether or not an output can be fired by an entity.
 *
 * @param entity        Entity's index.
 * @param output        Output's name.
 * @error               Invalid entity index.
 * @return              True if the output can be fired, false otherwise.
 */
bool EntityIO_HasEntityOutput(int entity, const char[] output);

/**
 * Retrieves an output's name from an entity.
 *
 * @param address        Output's address.
 * @param output         Buffer to store the output's name.
 * @param maxLen         Maximum length of string buffer.
 * @error                Invalid address.
 * @return               Number of cells written.
 */
int EntityIO_GetEntityOutputName(Address address, char[] output, int maxLen);

/**
 * Retrieves an output's offset from an entity.
 *
 * @param address        Output's address.
 * @error                Invalid address.
 * @return               Output's offset.
 */
int EntityIO_GetEntityOutputOffset(Address address);
```

## Output Actions
```sourcepawn
/**
 * Retrieves the first action's address from an entity's output.
 *
 * @param entity         Entity's index.
 * @param offset         Output's offset.
 * @param address        Action's address.
 * @error                Invalid entity index, invalid output offset.
 * @return               True if an action was found, false otherwise.
 */
bool EntityIO_FindEntityFirstOutputAction(int entity, int offset, Address& address);

/**
 * Retrieves the next action's address from an entity's output.
 *
 * @param address        Action's address.
 * @error                Invalid address.
 * @return               True if an action was found, false otherwise.
 */
bool EntityIO_FindEntityNextOutputAction(Address& address);

/**
 * Adds an action to an entity's output.
 *
 * @param entity             Entity's index.
 * @param output             Output's name.
 * @param target             Action's target.
 * @param input              Action's input.
 * @param param              Action's parameter.
 * @param delay              Action's delay.
 * @param timesToFire        Action's times to fire, -1 for infinite times.
 * @return                   True if the action has been added, false otherwise.
 * @error                    Invalid entity index.
 */
bool EntityIO_AddEntityOutputAction(int entity, const char[] output, const char[] target, const char[] input, const char[] param, float delay, int timesToFire);

/**
 * Retrieves an action's target from an entity's output.
 *
 * @param address        Action's address.
 * @param target         Buffer to store the action's target.
 * @param maxLen         Maximum length of string buffer.
 * @error                Invalid address.
 * @return               Number of cells written.
 */
int EntityIO_GetEntityOutputActionTarget(Address address, char[] target, int maxLen);

/**
 * Retrieves an action's input from an entity's output.
 *
 * @param address        Action's address.
 * @param input          Buffer to store the action's input.
 * @param maxLen         Maximum length of string buffer.
 * @error                Invalid address.
 * @return               Number of cells written.
 */
int EntityIO_GetEntityOutputActionInput(Address address, char[] input, int maxLen);

/**
 * Retrieves an action's parameter from an entity's output.
 *
 * @param address        Action's address.
 * @param param          Buffer to store the action's parameter.
 * @param maxLen         Maximum length of string buffer.
 * @error                Invalid address.
 * @return               Number of cells written.
 */
int EntityIO_GetEntityOutputActionParam(Address address, char[] param, int maxLen);

/**
 * Retrieves an action's remaining times to fire from an entity's output.
 *
 * @param address        Action's address.
 * @error                Invalid address.
 * @return               Action's remaining times to fire.
 */
int EntityIO_GetEntityOutputActionTimesToFire(Address address);

/**
 * Retrieves an action's ID from an entity's output.
 *
 * @param address        Action's address.
 * @error                Invalid address.
 * @return               Action's ID.
 */
int EntityIO_GetEntityOutputActionID(Address address);

/**
 * Retrieves an action's delay from an entity's output.
 *
 * @param address        Action's address.
 * @error                Invalid address.
 * @return               Action's delay.
 */
float EntityIO_GetEntityOutputActionDelay(Address address);
```

# Examples
## Inputs
```sourcepawn
	Address dataMap, address;
	if (EntityIO_FindEntityFirstInput(entity, dataMap, address))
	{
		do
		{
			char output[256];
			EntityIO_GetEntityInputName(address, output, sizeof(output));
			
			PrintToServer("Input: %s", output);
			
		} while (EntityIO_FindEntityNextInput(dataMap, address));
	}
}
```

## Outputs
```sourcepawn
	Address dataMap, address;
	if (EntityIO_FindEntityFirstOutput(entity, dataMap, address))
	{
		do
		{
			char output[256];
			EntityIO_GetEntityOutputName(address, output, sizeof(output));
			
			PrintToServer("Output: %s (Offset: %d)", output, EntityIO_GetEntityOutputOffset(address));
			
		} while (EntityIO_FindEntityNextOutput(dataMap, address));
	}
}
```

## Output Actions
```sourcepawn
public void OnPluginStart()
{
	HookEntityOutput("func_button", "OnPressed", Output_OnEntityOutput);
}

public void Output_OnEntityOutput(const char[] output, int caller, int activator, float delay)
{
	if (!IsValidEntity(caller))
	{
		return;
	}
	
	int offset = EntityIO_FindEntityOutputOffset(entity, output);
	if (offset == -1)
	{
		return;
	}
	
	Address address;
	if (EntityIO_FindEntityFirstOutputAction(entity, offset, address))
	{
		do
		{
			char target[256];
			EntityIO_GetEntityOutputActionTarget(address, target, sizeof(target));
			
			char input[256];
			EntityIO_GetEntityOutputActionInput(address, input, sizeof(input));
			
			char param[256];
			EntityIO_GetEntityOutputActionParam(address, param, sizeof(param));
			
			PrintToServer("Action: %s %s:%s:%s:%f:%d (Id: %d)", output, target, input, param, EntityIO_GetEntityOutputActionDelay(address), EntityIO_GetEntityOutputActionTimesToFire(address), EntityIO_GetEntityOutputActionID(address));
			
		} while (EntityIO_FindEntityNextOutputAction(address));
	}
}
```
