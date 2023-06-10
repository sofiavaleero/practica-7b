## PRACTICA 7b

# CODIGO:

```cpp
#define SD_CS          5
#define SPI_MOSI      23
#define SPI_MISO      19
#define SPI_SCK       18
#define I2S_DOUT      25
#define I2S_BCLK      27
#define I2S_LRC       26

Audio audio;

void setup(){
    pinMode(SD_CS, OUTPUT);
    digitalWrite(SD_CS, HIGH);
    SPI.begin(SPI_SCK, SPI_MISO, SPI_MOSI);
    Serial.begin(115200);
    SD.begin(SD_CS);
    audio.setPinout(I2S_BCLK, I2S_LRC, I2S_DOUT);
    audio.setVolume(10); // 0...21
    audio.connecttoFS(SD, "DSWeHRIILZ4.wav");
}

void loop(){
    audio.loop();
}

// optional
void audio_info(const char *info){
    Serial.print("info        "); Serial.println(info);
}
void audio_id3data(const char *info){  //id3 metadata
    Serial.print("id3data     ");Serial.println(info);
}
void audio_eof_mp3(const char *info){  //end of file
    Serial.print("eof_mp3     ");Serial.println(info);
}
void audio_showstation(const char *info){
    Serial.print("station     ");Serial.println(info);
}
void audio_showstreaminfo(const char *info){
    Serial.print("streaminfo  ");Serial.println(info);
}
void audio_showstreamtitle(const char *info){
    Serial.print("streamtitle ");Serial.println(info);
}
void audio_bitrate(const char *info){
    Serial.print("bitrate     ");Serial.println(info);
}
void audio_commercial(const char *info){  //duration in sec
    Serial.print("commercial  ");Serial.println(info);
}
void audio_icyurl(const char *info){  //homepage
    Serial.print("icyurl      ");Serial.println(info);
}
void audio_lasthost(const char *info){  //stream URL played
    Serial.print("lasthost    ");Serial.println(info);
}
void audio_eof_speech(const char *info){
    Serial.print("eof_speech  ");Serial.println(info);
}

```


# FUNCIONAMIENTO Y PUERTO SERIE

En este apartado buscamos configurar la ESP32 para reproducir un archivo WAVE almacenado en una SD externa. Controlar la reproducción y enviar los datos al amplificador. 

La salida por el puerto serie es para mostrar la información y mensajes de la raproducción de audio. 

En el setup establecemos los pines, inicializamos la comunicación en serie, la tarjeta SD y establecemos la configuración de audio, el volumen de reproducción y conectamos el audio con la SD y el archivo. 

En el loop unicamente ejecutamos la función audio.loop(). Lo que hace aquí es manejar la reproducción del archivo y realiza la lectura de datos y los envía a través de la I2S. 

Las funciones declaradas al final del codigo las utilizamos para imprimir información adicional sobre la reproducción de audio y proporcionar retroalimentación al usuario a través del puerto serie. 