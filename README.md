# SampleTestApp
# First-Android-Practice

사용 언어 : Kotlin

목적 : 코틀린 문법 익히기, 안드로이드 네비게이션 익히기

## Navigation → JetPack - navigation 사용

1. 프로젝트 디렉토리의 build.gradle에 jetpack 의존성을 추가한다
    
    ```
    dependencies {
      val nav_version = "2.5.0"
    
      // Kotlin
      implementation("androidx.navigation:navigation-fragment-ktx:$nav_version")
      implementation("androidx.navigation:navigation-ui-ktx:$nav_version")
    }
    ```
    
2. 네비게이션 패키지 생성(resource type = navigation) 하고 내부에 navigation resouece file을 생성한다.
    
    <img width="613" alt="image" src="https://user-images.githubusercontent.com/71999370/181243751-b330f768-a04b-4bcb-96a0-e3183bfac772.png">

    
3. NavHostFragment를 추가한다
    
    activity_main.xml에 다음코드를 추가하여 NavHostFragment를 추가한다(ConstraingLayout 태그 하위항목에 추가)
    
    ```xml
    <androidx.fragment.app.FragmentContainerView
            android:id="@+id/nav_host_fragment"
            android:name="androidx.navigation.fragment.NavHostFragment"
            android:layout_width="0dp"
            android:layout_height="0dp"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            app:layout_constraintBottom_toBottomOf="parent"
    
            app:defaultNavHost="true"
            app:navGraph="@navigation/nav_graph" />
    ```
    
4. 네비게이션 그래프를 확인

네비게이션은 총 세가지 파트로 나누어 진다.

1. **Navigation graph (XML Resource)**
    
    <img width="804" alt="image" src="https://user-images.githubusercontent.com/71999370/181243828-fdba5245-1364-4634-b45d-1601db67a456.png">

    
    네비게이션 그래프에는 모든 정보가 모여있다고 할 수 있다. XML 코드로도 확인할 수 있다. 
    
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <navigation xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/nav_graph"
        app:startDestination="@id/mainFragment">
    
        <fragment
            android:id="@+id/mainFragment"
            android:name="com.example.sampletestapp.fragment.MainFragment"
            android:label="fragment_main"
            tools:layout="@layout/fragment_main" >
            <action
                android:id="@+id/action_mainFragment_to_questionFragment"
                app:destination="@id/questionFragment" />
        </fragment>
    ...
    </navigation>
    ```
    
    프래그먼트를 생성하면 자동으로 비어있는 레이아웃이 생성된다. 그리고 각 레이아웃을 디자인하고 네비게이션 그래프에서 각 레이아웃으로부터 destination이라는 이름을 가지고 이동하고 싶은 곳으로 연결할 수 있다.
    
    - 그래프를 연결함에 따라 각 프래그먼트의 action id와 destination이 결정됨
    - 이러한 정보를 바탕으로 navController가 호출되었을 때 액션이 정의됨
    
2. NavHostFragment **(Layout XML view) → 프레그먼트 네비게이션을 위한 빈 위젯**
3.  NavController (Kotlin / Java object)
    
    네비게이션을 컨트롤한다. NavHostFragment는 개별적으로 NavController를 가지고 있으며. 네비게이션 그래프 정보를 바탕으로 네비게이션 간 이동(액션)을 담당.
