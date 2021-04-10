<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/log"
        android:layout_marginTop="200dp"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="INU_Login"
        android:textSize="30sp"/>

    <TextView
        android:id="@+id/tv1"
        android:layout_marginTop="20dp"
        app:layout_constraintTop_toBottomOf="@id/log"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_height="wrap_content"
        android:layout_width="50dp"

        android:hint="닉네임                      "/>

    <ImageView
        android:layout_width="200dp"
        android:layout_height="30dp"
        android:layout_marginTop="20dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@id/log"
        android:src="@drawable/edit_text_background"/>

    <TextView
        android:layout_marginTop="10dp"
        app:layout_constraintTop_toBottomOf="@id/tv1"
        app:layout_constraintStart_toStartOf="@id/tv1"
        android:id="@+id/texrview"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:background="@drawable/edit_text_background"
        android:inputType="numberPassword"/>

    <TextView
        android:id="@+id/text2"
        app:layout_constraintTop_toBottomOf="@id/texrview"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textColor="#FF0000"
        android:text="아이디 또는 비밀번호가 일치하지 않습니다."/>
    <TextView
        android:id="@+id/text3"
        android:layout_marginTop="10dp"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@id/text2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="아이디/비밀번호 찾기"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:text="로그인"
        app:layout_constraintEnd_toEndOf="parent"
        android:background=""
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/text3"
        android:background="@drawable/btn_background"/>


</androidx.constraintlayout.widget.ConstraintLayout>
