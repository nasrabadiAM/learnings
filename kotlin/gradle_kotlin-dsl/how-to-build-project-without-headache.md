How To build Android Kotlin DSL Gradle project without headache
---

if You download an Android Project which is based on Gradle Kotlin DSl and try build it with Android studio, it will probably fail, and will not detect android project.
 

 To Fix this problem, follow steps below:

 Step 1: Clone Your Project.

 First Of all Clone the project you want to build.


 Step 2: build it from terminal using this command,

 ```
	./gradlew assembleDebug --info
 ```

 Step 3:
 open project via Android studio and then build project with it.


 Step 4: 
 Define App Module to Run the app.

