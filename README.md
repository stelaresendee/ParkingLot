CÓDIGO TELA CADASTRO:

package com.example.parkinglots

import android.annotation.SuppressLint
import android.content.Intent
import android.os.Bundle
import android.text.Editable
import android.text.TextWatcher
import android.text.method.PasswordTransformationMethod
import android.widget.Button
import android.widget.EditText
import android.widget.Switch
import android.widget.TextView
import android.widget.Toast
import androidx.activity.enableEdgeToEdge
import androidx.appcompat.app.AppCompatActivity
import androidx.core.view.ViewCompat
import androidx.core.view.WindowInsetsCompat

class tela_cadastro : AppCompatActivity() {
    @SuppressLint("MissingInflatedId")

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_tela_cadastro)
        var Senha: EditText = findViewById(R.id.editTextTextPassword)
        var VSenha: Switch = findViewById(R.id.switch1)
        var Senha2: EditText = findViewById(R.id.edtConfirmar)
        var VSenha2: Switch = findViewById(R.id.switch2)
        var txtEntrar = findViewById<TextView>(R.id.txtEntrar)
        var edtNome: EditText = findViewById(R.id.edtNomeCadastro)
        var edtSobrenome: EditText = findViewById(R.id.edtSobrenome)
        var edtEmail: EditText = findViewById(R.id.EdtEmailCadastro)
        var edtContato: EditText = findViewById(R.id.edtContato)
        var Cadastro: Button = findViewById(R.id.btnCriarCadastro)
        txtEntrar.setOnClickListener { TelaLogin() }

        Cadastro.setOnClickListener {
            val inputText = edtNome.text.toString().trim()
            val inputText2 = edtSobrenome.text.toString().trim()
            val inputText3 = edtEmail.text.toString().trim()
            val inputText4 = edtContato.text.toString().trim()
            val inputText5 = Senha.text.toString().trim()
            val inputText6 = Senha2.text.toString().trim()

            if (inputText.isEmpty() || inputText2.isEmpty() || inputText3.isEmpty() || inputText4.isEmpty() || inputText5.isEmpty() || inputText6.isEmpty()) {
                Toast.makeText(this, "Preencha corretamente os campos acima.", Toast.LENGTH_SHORT).show()
            } else {
                Toast.makeText(this, "Conta criada com sucesso!", Toast.LENGTH_SHORT).show()
                startActivity(Intent(this,MainActivity::class.java))
            }
        }

        VSenha.setOnCheckedChangeListener{_, isChecked ->
            if (isChecked) {

                Senha.transformationMethod = null
            } else {

                Senha.transformationMethod = PasswordTransformationMethod.getInstance()
            }
        }
        Senha.addTextChangedListener(object : TextWatcher {
            override fun afterTextChanged(s: Editable?) {}

            override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {}

            override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {

                val selectionStart: Int = Senha.selectionStart
                val selectionEnd: Int = Senha.selectionEnd


                Senha.transformationMethod =
                    if (VSenha.isChecked) null else PasswordTransformationMethod.getInstance()


                Senha.setSelection(selectionStart, selectionEnd)
            }
        })
        VSenha2.setOnCheckedChangeListener{_, isChecked ->
            if (isChecked) {

                Senha2.transformationMethod = null
            } else {

                Senha2.transformationMethod = PasswordTransformationMethod.getInstance()
            }
        }
        Senha2.addTextChangedListener(object : TextWatcher {
            override fun afterTextChanged(s: Editable?) {}

            override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {}

            override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {

                val selectionStart: Int = Senha2.selectionStart
                val selectionEnd: Int = Senha2.selectionEnd


                Senha2.transformationMethod =
                    if (VSenha2.isChecked) null else PasswordTransformationMethod.getInstance()


                Senha2.setSelection(selectionStart, selectionEnd)
            }
        })
    }
    fun TelaLogin(){
        startActivity(Intent(this,MainActivity::class.java))
    }
}
