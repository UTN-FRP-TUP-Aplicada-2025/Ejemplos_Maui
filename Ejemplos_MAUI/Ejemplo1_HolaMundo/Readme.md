
## Descripción

proyecto de prueba


### Solución páginas de 16kb 

```
	<!-- Configuración base para Android con soporte 16KB -->
	<PropertyGroup Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'android'">
		<!-- Soporte obligatorio para páginas de 16 KB -->
		<AndroidLdFlags>-Wl,-z,max-page-size=16384</AndroidLdFlags>

		<!-- Solo arm64 es requerido para 16KB, pero puedes incluir otros ;android-x86_64-->
		<RuntimeIdentifiers>android-arm64</RuntimeIdentifiers>

		<AndroidPackageFormat Condition="'$(Configuration)' == 'Debug'">apk</AndroidPackageFormat>
		<AndroidCreatePackagePerAbi Condition="'$(Configuration)' == 'Debug'">false</AndroidCreatePackagePerAbi>

		<AndroidPackageFormat Condition="'$(Configuration)' == 'Release'">aab</AndroidPackageFormat>
		<AndroidCreatePackagePerAbi Condition="'$(Configuration)' == 'Release'">false</AndroidCreatePackagePerAbi>

		<AndroidUseAapt2>true</AndroidUseAapt2>
		
		<!-- None|Full|SdkOnly -->
		<AndroidLinkMode>None</AndroidLinkMode>		
	</PropertyGroup>
```


### Manifiesto de android

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
	
	<application android:allowBackup="true" android:icon="@mipmap/appicon" 
				 android:roundIcon="@mipmap/appicon_round" android:supportsRtl="true">		
	</application>
	
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	<uses-permission android:name="android.permission.INTERNET" />

	<uses-sdk android:minSdkVersion="21" android:targetSdkVersion="33" />
</manifest>
```