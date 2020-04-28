# Chamada de vídeo com Jitsi Meet - App em react native

Como utilizar o Jisti Meet em um projeto com react native - android?

Instale o pacote no seu projeto:
yarn add react-native-jitsi-meet --save

1) Em android/app/build.gradle, adicione ou substitua as linhas

project.ext.react = [
    entryFile: "index.js",
    bundleAssetName: "app.bundle",
    enableHermes: false,
]


2) Em android/app/src/main/java/com/NOME_DO_SEU_PROJETO/MainApplication.java 
adicione ou substitua os métodos:

    @Override
    protected String getJSMainModuleName() {
      return "index";
    }

    @Override
    protected @Nullable String getBundleAssetName() {
      return "app.bundle";
    }


3) Em android/build.gradle, substitua o código:

    allprojects {
    repositories {
        mavenLocal()
        maven {
            // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
            url("$rootDir/../node_modules/react-native/android")
        }
        
        maven {
            url "https://github.com/jitsi/jitsi-maven-repository/raw/master/releases"
        }

        maven {
            // Android JSC is installed from npm
            url("$rootDir/../node_modules/jsc-android/dist")
        }

        google()
        jcenter()
        maven { url 'https://jitpack.io' }
    }
}

4) Em android/app/build.gradle, adicione as dependências:

packagingOptions {
        pickFirst "lib/armeabi-v7a/libc++_shared.so"
        pickFirst "lib/armeabi-v7a/libjsc.so"
        pickFirst "lib/arm64-v8a/libc++_shared.so"
        pickFirst "lib/arm64-v8a/libjsc.so"
        pickFirst "lib/x86/libjsc.so"
        pickFirst "lib/x86/libc++_shared.so"
        pickFirst "lib/x86_64/libc++_shared.so"
    }


5) Em AndroidManifest.xml debug, substitua a linha:


    <application android:allowBackup="true" tools:replace="android:allowBackup" android:usesCleartextTraffic="true" tools:targetApi="28" tools:ignore="GoogleAppIndexingWarning" />

6) No arquivo android/build.gradle, verifique o campo minSdkVersion, ele deve ser no mínimo:
minSdkVersion = 21
