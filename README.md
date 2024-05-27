CÓDIGO TELA CADASTRO:

package com.example.parkinglots

import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import android.content.Intent
import android.text.Editable
import android.text.TextWatcher
import android.text.method.PasswordTransformationMethod
import android.widget.Button
import android.widget.EditText
import android.widget.Switch
import android.widget.TextView
import android.widget.Toast

class tela_cadastro : AppCompatActivity() {
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
        val edtContato: EditText = findViewById(R.id.edtContato)
        edtContato.addTextChangedListener(PhoneNumberFormattingTextWatcher(edtContato))
        var Cadastro: Button = findViewById(R.id.btnCriarCadastro)
        txtEntrar.setOnClickListener { TelaLogin() }

        Cadastro.setOnClickListener {
            val inputText = edtNome.text.toString().trim()
            val inputText2 = edtSobrenome.text.toString().trim()
            val inputText3 = edtEmail.text.toString().trim()
            val inputText4 = edtContato.text.toString().trim()
            val inputText5 = Senha.text.toString().trim()
            val inputText6 = Senha2.text.toString().trim()
            val nome = edtNome.text.toString()
            val sobrenome = edtSobrenome.text.toString()
            val email = edtEmail.text.toString()
            val numero = edtContato.text.toString()


            if (inputText5 != inputText6){
                Toast.makeText(this, "Verifique se as senhas estão iguais.",Toast.LENGTH_SHORT).show()
            }
            else if (inputText.isEmpty() || inputText2.isEmpty() || inputText3.isEmpty() || inputText4.isEmpty() || inputText5.isEmpty() || inputText6.isEmpty()) {
                    Toast.makeText(this, "Preencha corretamente os campos acima,", Toast.LENGTH_SHORT).show()
                }
            else {

                val intent = Intent(this,tela_minha_conta::class.java)
                intent.putExtra("NOME", nome)
                intent.putExtra("SOBRENOME", sobrenome)
                intent.putExtra("EMAIL", email)
                intent.putExtra("SOBRENOME", sobrenome)
                intent.putExtra("NUMERO", numero)
                startActivity(intent)
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
    class PhoneNumberFormattingTextWatcher(private val edtContato: EditText) : TextWatcher {
        private var isFormatting: Boolean = false

        override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {}

        override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {}

        override fun afterTextChanged(editable: Editable?) {
            if (isFormatting) {
                return
            }

            isFormatting = true

            val phoneNumber = editable.toString().replace("[^\\d]".toRegex(), "")

            // Aplica a máscara de telefone
            if (phoneNumber.length >= 11) {
                val formattedPhoneNumber = "(${phoneNumber.substring(0, 2)}) ${phoneNumber.substring(2, 7)}-${phoneNumber.substring(7)}"
                edtContato.setText(formattedPhoneNumber)
                edtContato.setSelection(formattedPhoneNumber.length)
            }

            isFormatting = false
        }
    }
}
