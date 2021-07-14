[![Maven Central](https://maven-badges.herokuapp.com/maven-central/io.github.justin-lewis/safestate/badge.svg?style=plastic)](https://maven-badges.herokuapp.com/io.github.justin-lewis/safestate)
# Safe State
An Android library for avoiding TransactionTooLargeException during state saving and restoration

## Getting Started

Check out the app directory for a sample app using this library

##### **Install**
Root build.gradle
```gradle
    allprojects {
		repositories {
			...
			mavenCentral()
		}
	}
```
App build.gradle
```gradle
    dependencies {
        implementation 'com.github.justin-lewis:safestate:1.0.0'
        ...
    }
```
##### **Usage**

Basic Initialize at application class
```kotlin
        class SafeStateSampleApp : Application() {
            override fun onCreate() {
                super.onCreate()
                SafeState.initialize(this)
                // Other logic code
            }
        }
```

At your base Activity class:
```kotlin
    override fun onRestoreInstanceState(savedInstanceState: Bundle) {
        SafeState.restoreInstanceState(this, savedInstanceState)
        super.onRestoreInstanceState(savedInstanceState)
        // real restore state. For example
        // bitmap = savedInstanceState.getParcelable(KEY_BITMAP)!!
    }

    override fun onSaveInstanceState(outState: Bundle) {
        super.onSaveInstanceState(outState)
        // real save state. For example
        // outState.putParcelable(KEY_BITMAP, outState)
        SafeState.saveInstanceState(this, outState)
    }
```

At your fragment state pager class
```
    class BannerPagerAdapter constructor(fragmentManager: FragmentManager) : SafeFragmentStatePagerAdapter(fragmentManager, BEHAVIOR_RESUME_ONLY_CURRENT_FRAGMENT)
```

## Issues and feedback
If there is specific issues, bugs, or feature requests please report in our [mailing list][mailing list]

## Contributor & Maintainer

- [Justin Lewis](https://github.com/justin-lewis) (Maintainer)
  
## License
[Apache License 2.0](https://gitlab.extremevn.vn/development-mobile-1/library/flutter_amplify_sdk/raw/master/LICENSE)

[mailing list]: https://groups.google.com/g/safestatehandler