//# Language
//make our app to support multiple languages
package com.example.language;

import androidx.appcompat.app.ActionBar;
import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.app.DatePickerDialog;
import android.content.DialogInterface;
import android.content.SharedPreferences;
import android.content.res.Configuration;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.LinearLayout;
import android.widget.RelativeLayout;
import android.widget.Spinner;
import android.widget.Toast;

import java.lang.reflect.Array;
import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    Button btn_change;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        loadLocal();
        setContentView(R.layout.activity_main);
        ActionBar actionBar = getSupportActionBar();
        actionBar.setTitle(getResources().getString(R.string.app_name));
        btn_change = findViewById(R.id.Btn_change);
        btn_change.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                showChangeLanguage();
            }
        });
    }

    private void showChangeLanguage() {
        final String[] listname = {"English", "Arabic"};
        AlertDialog.Builder mBulider = new AlertDialog.Builder(MainActivity.this);
        mBulider.setTitle("Change Language");
        mBulider.setSingleChoiceItems(listname, -1, new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                if (which == 0) {
                    setLocal("En");
                    recreate();
                } else if (which == 1) {
                    setLocal("Ar");
                    recreate();
                }

                dialog.dismiss();
            }
        });
        AlertDialog mDialog = mBulider.create();
        mDialog.show();
    }

    private void setLocal(String ar) {
        Locale locale = new Locale(ar);
        Locale.setDefault(locale);
        Configuration config = new Configuration();
        config.locale = locale;
        getBaseContext().getResources().updateConfiguration(config, getBaseContext().getResources().getDisplayMetrics());
        SharedPreferences.Editor editor = (SharedPreferences.Editor) getSharedPreferences("Settings", MODE_PRIVATE);
        editor.putString("MY_lang", ar);
        editor.apply();
    }


    public void loadLocal() {
        SharedPreferences prefs = getSharedPreferences("Settings", MODE_PRIVATE);
        String language = prefs.getString("MY_lang", "");
        setLocal(language);
    }

}
