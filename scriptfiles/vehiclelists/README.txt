The base vehicle list has been added to the 0.2X server distribution
for anyone that may have current use for them.

The following people have contributed to the SA-MP base vehicle list :-

FILENAME	 AUTHOR			CURRENT REVISION

bone.txt 	: Simon			: 1.2
flint.txt 	: kenny01		: 1.4
lv_airport.txt	: Alex			: 1.1
lv_law.txt	: damospiderman		: 1.4
lv_gen.txt	: damospiderman		: 1.5
whetstone.txt	: Wacko			: 1.2
sf_gen.txt	: dugi			: 2.6
sf_airport.txt	: dugi			: 1.4
sf_law.txt	: dugi			: 1.9
tierra.txt	: Kye 			: 1.2
red_county.txt	: Trix			: 1.2
ls_law.txt	: jax 			: 1.1
ls_gen_inner.txt: jax 			: 1.3
ls_gen_outer.txt: jax 			: 1.3
ls_airport.txt	: jax 			: 1.0


-------------------------------------------------------------------

Below is a useful function for loading static vehicles from a desired file :-

Example calling from your OnGameModeInit() callback:

-------------------------------------------------------------------

new total_vehicles_from_files=0;

total_vehicles_from_files += LoadStaticVehiclesFromFile("vehiclelists/bone.txt");
total_vehicles_from_files += LoadStaticVehiclesFromFile("vehiclelists/flint.txt");
total_vehicles_from_files += LoadStaticVehiclesFromFile("vehiclelists/tierra.txt");

-------------------------------------------------------------------

LoadStaticVehiclesFromFile(const filename[])
{
	new File:file_ptr;
	new line[256];
	new var_from_line[64];
	new vehicletype;
	new Float:SpawnX;
	new Float:SpawnY;
	new Float:SpawnZ;
	new Float:SpawnRot;
    	new Color1, Color2;
	new index;
	new vehicles_loaded;
    
	file_ptr = fopen(filename,filemode:io_read);
	if(!file_ptr) return 0;
	
	vehicles_loaded = 0;

	while(fread(file_ptr,line,256) > 0)
	{
	    index = 0;
	    
	    // Read type
  		index = token_by_delim(line,var_from_line,',',index);
  		if(index == (-1)) continue;
  		vehicletype = strval(var_from_line);
   		if(vehicletype < 400 || vehicletype > 611) continue;
  		
  		// Read X, Y, Z, Rotation
  		index = token_by_delim(line,var_from_line,',',index+1);
  		if(index == (-1)) continue;
  		SpawnX = floatstr(var_from_line);

  		index = token_by_delim(line,var_from_line,',',index+1);
  		if(index == (-1)) continue;
  		SpawnY = floatstr(var_from_line);

  		index = token_by_delim(line,var_from_line,',',index+1);
  		if(index == (-1)) continue;
  		SpawnZ = floatstr(var_from_line);

  		index = token_by_delim(line,var_from_line,',',index+1);
  		if(index == (-1)) continue;
  		SpawnRot = floatstr(var_from_line);

  		// Read Color1, Color2
  		index = token_by_delim(line,var_from_line,',',index+1);
  		if(index == (-1)) continue;
  		Color1 = strval(var_from_line);

  		index = token_by_delim(line,var_from_line,';',index+1);
  		Color2 = strval(var_from_line);

  		//printf("%d|%f|%f|%f|%f|%d|%d",vehicletype,
  		    //SpawnX,SpawnY,SpawnZ,SpawnRot,Color1,Color2);
  		    
		AddStaticVehicleEx(vehicletype,SpawnX,SpawnY,SpawnZ,SpawnRot,Color1,Color2,-1);
		
		vehicles_loaded++;
	}
	
	fclose(file_ptr);
	printf("Loaded %d vehicles from: %s",vehicles_loaded,filename);
	return vehicles_loaded;
}

-------------------------------------------------------------------

// Tokenise by a delimiter
// Return string and index of the end determined by the
// provided delimiter in delim
token_by_delim(const string[], return_str[], delim, start_index)
{
	new x=0;
	while(string[start_index] != EOS && string[start_index] != delim) {
	    return_str[x] = string[start_index];
	    x++;
	    start_index++;
	}
	return_str[x] = EOS;
	if(string[start_index] == EOS) start_index = (-1);
	return start_index;
}

-------------------------------------------------------------------