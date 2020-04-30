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


    Button btn_change ;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

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
        mBulider.setTitle("Change Language...");
        mBulider.setSingleChoiceItems(listname, 2, new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                if (which == 0) {
                    setAppLocale("en");
                    recreate();
                } else if (which == 1) {
                    setAppLocale("ar");
                    recreate();
                }

                dialog.dismiss();
            }
        });
        AlertDialog mDialog = mBulider.create();
        mDialog.show();
    }

    private void setAppLocale(String language){
        Locale locale=new Locale(language);
        Locale.setDefault(locale);
        Configuration configuration=new Configuration();
        configuration.locale=locale;
        getBaseContext().getResources().updateConfiguration(configuration,getBaseContext().getResources().getDisplayMetrics());
        setContentView(R.layout.activity_main);

    }


}
