"Cora Social Explora"

Project Overview
This Android application is developed for IMAD Assignment 1. The app helps users stay socially active by providing specific "Social Sparks" (interaction suggestions) based on the time of day they select.

Key Features
* Time Selection: A dropdown menu (Spinner) to choose a time of day.
* Smart Messages: Social gesture that recomendation for the selected time of day.
* Reset Logic: A reset button that resets the time of day.

Technical Details
* Language: Kotlin
* IDE: Android Studio
* Components: Spinner, Button, TextView. 

Author
JB Eksteen

Youtube Video LINK: https://youtube.com/shorts/IiSffDiu02M


MainActivity.kt
package com.example.cora_explora_30

import android.os.Bundle
import android.view.View
import android.widget.AdapterView
import android.widget.Button
import android.widget.Spinner
import android.widget.TextView
import androidx.activity.enableEdgeToEdge
import androidx.appcompat.app.AppCompatActivity
import androidx.core.view.ViewCompat
import androidx.core.view.WindowInsetsCompat

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContentView(R.layout.activity_main)

        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main)) { v, insets ->
            val systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars())
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom)
            insets
        }

        // 1. Identify all 3 components from your Design Tab
        val timeSpinner = findViewById<Spinner>(R.id.time_spinner)
        val resetButton = findViewById<Button>(R.id.reset_button)
        val messageTextView = findViewById<TextView>(R.id.messageTextView)

        // 2. Set up the Reset Button
        resetButton.setOnClickListener {
            timeSpinner.setSelection(0)
            messageTextView.text = "" // This clears the message
        }

        // 3. Set up the logic for selecting a time
        timeSpinner.onItemSelectedListener = object : AdapterView.OnItemSelectedListener {
            override fun onItemSelected(parent: AdapterView<*>, view: View?, position: Int, id: Long) {

                // This 'when' block matches the position to your specific text
                val sparkMessage = when (position) {
                    1 -> "Send a 'good morning' text to a family member."
                    2 -> "Reach out to a colleague with a quick 'thank you'."
                    3 -> "Share a funny meme or video with a friend."
                    4 -> "Send a quick 'thinking of you' message."
                    5 -> "Call a friend or relative for a quick 5-min catch up."
                    6 -> "Leave a thoughtful comment on a friend's post."
                    else -> "" // Position 0 (Select Time...) shows nothing
                }

                // This puts the message into the TextView on your screen
                messageTextView.text = sparkMessage
            }

            override fun onNothingSelected(parent: AdapterView<*>) {
                // Required but unused
            }
        }
    }
}



activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="1.0"
        app:srcCompat="@drawable/cora_background_image" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="cursive"
        android:gravity="center"
        android:text="Cora Social Explora"
        android:textSize="48sp"
        android:textStyle="bold"
        tools:layout_editor_absoluteX="31dp"
        tools:layout_editor_absoluteY="44dp" />

    <Spinner
        android:id="@+id/time_spinner"
        android:layout_width="350dp"
        android:layout_height="50dp"
        android:entries="@array/time_slots"
        app:layout_constraintBottom_toBottomOf="@+id/imageView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.508"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/imageView"
        app:layout_constraintVertical_bias="0.287" />

    <Button
        android:id="@+id/reset_button"
        android:layout_width="133dp"
        android:layout_height="66dp"
        android:layout_marginBottom="92dp"
        android:backgroundTint="#000000"
        android:text="Reset Time"
        app:layout_constraintBottom_toBottomOf="@+id/imageView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent" />

    <TextView
        android:id="@+id/messageTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="348dp"
        android:gravity="center"
        android:text="What should I send?"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="@+id/imageView"
        app:layout_constraintStart_toStartOf="@+id/imageView" />
</androidx.constraintlayout.widget.ConstraintLayout>


time_slots.xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="time_slots">
        <item>select Time of Day</item>
        <item>morning</item>
        <item>mid-morning</item>
        <item>afternoon</item>
        <item>afternoon snack time</item>
        <item>dinner</item>
        <item>after dinner/night</item>
    </string-array>
</resources>
