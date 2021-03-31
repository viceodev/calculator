<template src="./assets/html/Calculator.html"></template>



<script>

export default{
    

    data(){
        return {
            test: 'hey there',
            elements:  document.querySelectorAll('div#element'),
            answer:  null,
            input: 'input',
            inputRegex: /[0-9.]/i,
            CalcRegex: /\W/,
            Calc: '',
            error: false
        }
    },

    mounted(){
        this.input = document.querySelector('div#input');
    },

    methods: {
        check_if_answer_exists(){
            if(this.answer != null){
                this.answer_exists = true;
            }
        },

        input_answer_in_page(){
            if(this.answer_exists == true){
                this.input.innerHTML = this.answer;
                this.answer = null;
                this.answer_exists = false;
            }
        },

        input_element(e){

            this.check_if_answer_exists();
            this.input_answer_in_page();
            
            if(this.inputRegex.test(e.target.textContent)){
                this.input.innerHTML += e.target.textContent;
            }else{
                this.input.innerHTML += ` ${e.target.textContent} `;                
            }

        },


        clear(){
            this.input.innerHTML = '';
        },

        backspace(){
            this.input.innerHTML = this.input.innerHTML.substr(0, (this.input.textContent.length - 1));
        },

        check_if_input_ends_with_calc(){
            if(this.input.textContent.split(' ')[this.input.textContent.split(' ').length - 1] == ''){
                alert('Syntax Error');
                this.error = true;
            }else{
                this.error = false;
            }
        },

        run_calculation(){
            if(this.error == false){
                this.answer = eval(this.splitted_input.join(' '));
                
                this.input.innerHTML += `<p id="answer">=${this.answer}</p>`;
            }
        },

        calc(){
            this.splitted_input = this.input.textContent.split(' ');
            this.check_if_input_ends_with_calc();
            this.run_calculation();
        }
    }

}
</script>



<style src="./assets/css/style.css"></style>