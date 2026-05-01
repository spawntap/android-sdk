
## Integrating the the SDK

#### Add these dependencies to your build.gradle

```gradle
dependencies {
    implementation 'com.github.spawntap:android-sdk:1.0.0'
}
```

#### Add these to your proguard-rules.pro (optional)

```gradle
-keep,allowobfuscation,allowshrinking class kotlin.coroutines.Continuation
-keep,allowobfuscation,allowshrinking interface retrofit2.Call
-keep,allowobfuscation,allowshrinking class retrofit2.Response
```

#### Add these to your settings.gradle file

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS) // make sure RepositoriesMode is set to FAIL_ON_PROJECT_REPOS
    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
        maven { url 'https://jitpack.io' } // make sure to add this line
    }
}
```

## Initialising the SDK

#### Java

```java
import com.spawntap.sdk.SpawnTapConfig;

public class BootActivity extends AppCompatActivity {

    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        String SPAWNTAP_SDK_KEY = "SPAWNTAP_SDK_KEY";
        String userId = "USER_ID";
        SpawnTapConfig spawnTapConfig = new SpawnTapConfig(SPAWNTAP_SDK_KEY);
        spawnTapConfig.setUserId(userId);
        Context context = this;
        SpawnTap.init(this, spawnTapConfig);
    }
}
```

#### Kotlin

```kotlin
import com.trackmyuser.sdk.TrackMyUser

class BootActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val SPAWNTAP_SDK_KEY = "SPAWNTAP_SDK_KEY"
        val userId = "USER_ID"

        val spawnTapConfig = SpawnTapConfig(SPAWNTAP_SDK_KEY).apply {
            setUserId(userId)
        }

        val context: Context = this
        SpawnTap.init(this, spawnTapConfig)
    }
}
```

## Opening the Offerwall

#### Java

```java
import com.trackmyuser.sdk.SpawnTap;
import com.trackmyuser.sdk.SpawnTapListener;

public class HomeActivity extends AppCompatActivity {

    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        
        Context ctx = getContext();

        SpawnTap.open(ctx, new SpawnTapListener() {
            @Override
            public void onSuccess() {
            }

            @Override
            public void onFailed(String error) {
                Toast.makeText(ctx, error, Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

#### Kotlin

```kotlin
import com.trackmyuser.sdk.TrackMyUser
import com.trackmyuser.sdk.TrackMyUserEvent

class HomeActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val ctx: Context = this

        SpawnTap.open(ctx, object : SpawnTapListener {
            override fun onSuccess() {
            }

            override fun onFailed(error: String) {
                Toast.makeText(ctx, error, Toast.LENGTH_SHORT).show()
            }
        })
    }
}
```
