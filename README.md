# Basic Android

# 0. 람다

1. 해당 뷰 클래스 오버라이딩 해야 하는 메서드가 1개 라면 사용가능
   - 특정 기능만 딱! 만들고자 한다면 람다를 사용해서 처리하는 것이 좋으나, 동일한 동작을 다른 뷰에서도 사용하고자 한다면 클래스로 만들어서 사용하는 것이 좋다. "의견"

<pre>
<code>
   button.seOnClickListener{ view -> 
      // 클릭시 발생시킬 무언가
      textView.text = "Hello, You clicked button."
   }
</code>
</pre>

2. 2개 이상이이라면 중첩 익명 클래스 사용가능
   - 특정 기능만 딱! 만들고자 한다면 람다를 사용하면 좋으나, 오버라이팅 해야 하는 함수가 2개 이상이라면 다음과 같이 익명 중첩 클래스를 사용하면 기능을 구현 할 수 있다.
   - 그러나 이렇게 할 것 이라면 클래스로 분리해 두는 것도 나빠 보이지는 않는다. 그런데 딱 그 뷰는 "특정 동작"을 하게 할 것이라면 이 방법이 좋아 보인다 "의견 - 람다와 사용 시기 동일 하다면"

<pre>
<code>
   //

   editText.addTextChangedListener(object : TextWatcher{
      override fun onTextChanged(s: CharSequence?, start : Int , before: Int, count: Int){
         textView.text = s 
      }
      override fun afterTextChanged(s: Editable?) {}

      override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {}  

   })
</code>
</pre>

3. 기본적으로는 중첩 클래스 사용하여 메서드 오버라이딩 가능

   - 여러 뷰에서 동일한 기능을 수행 하게 만들고자 한다면, 클래스로 만들어서 이벤트를 등록 하는 방식이 좋다.

<pre>
<code>
   

   var listener3 = BtnLisnter3()
   button3.setOnClickListener(listener3) // 다음과 같이 클래스로 만든 이벤트를 등록해준다?
   button4.setOnClickListener(listener3)

   inner class BtnLisnter3 : View.OnClickListener {
        override fun onClick(v: View?) {
            when (v?.id) {
                R.id.button3 -> {
                    textView.text = "세 번째 버튼을 눌렀습니다."
                }
                R.id.button4 -> {
                    textView.text = "네 번째 버튼을 눌렀습니다."
                }
            }
        }
    }
</code>
</pre>

# 1. 안드로이드

1. Android Runtime (ART)
2. Core Libraries

# 2. 안드로이드 스튜디오

1. 디렉토리 환경에서는 한글이 들어가지 않도록 주의 한다.

# 3. Activity 화면을 의미 한다. web : html 이라고 생각

1. Name 앱이름 : 첫 글자는 영문 대무자로 하는 것을 추천한다.
2. Package name : 조직의 주소 같이 겹치지 않은 무언가. : 소문자로 시작을 추천한다.
   <br/> -> 앱이름이 동일할 경우 package 이름으로도 구분 자를 사용
3. Save location : 프로젝트가 저장될 경로
4. 빌드 툴 : (Gradle)
5. AVD : 안드로이드 가상 머신

## 4. 용어 정리

1. 액티비티 : 전체화면
2. 뷰(ui 구성) - dom과 비슷 : 액티비티 안의 구성요소 -> 배치하는 것 "레이아웃"
3. 위젯 : 컨트롤 요소
4. 뷰 그룹 : 뷰를 여러개 가지고 있는 뷰

# 5. View

1. 안드로이드에서 눈에 보이는 모든 요소를 "뷰"하고 부르며 개발자가 배치한 모든 뷰들은 class로 제공되는데 view라는 클래스를 상속받고 있다.
2. 뷰 클래스는 모든 ui요소들의 부모클래스로써 위젝과 레이아웃으로 나뉜다.

### 1. 레이아웃

1. 컨테이너, 뷰 그룸이라고 부르기도 하며 다른 뷰 들을 포함 하고 (컨테이너) 내부의 뷰를 통합 관리하고 (뷰 그룸) 내부의 뷰들이 배치되는 모양을 결정(레이아웃)한다.

### 2. 위젯

1. 문자열 입력, 분자열 출력 등 어떤 기능을 가지고 있고 사용자와 상호작용 하는 뷰들을 통칭해서 위젯이라고 부른다.

### 3. 화면 만들기

1. 안드로이드는 화면에 레이아웃을 배치하고 그 안에 다른 레이 아웃이나 위젝을 배치하여 화면의 모양을 만든다.
2. 이렇게 만들어진 화면은 모두 객체로 만들어지며 개발자는 이 객체들을 이용해 코드에서 필요한 작업을 할 수 있다.

### 4. View 속성

0. layout 뷰자체
1. id: xml이나 코튼린 코드에서 view에 접근하기 위해서 사용하는 이름입니다.
1. layout_width : 뷰의 가로 길이 [ match_parent : 자기가 있는 환경에 꽉 채우겠다.]
1. layout_height: 뷰의 세로 길이 [ wrap_parent : 자신의 속성을 최대한 보여줄 수 있는 크기 입니다.]
1. layout_margin : 뷰의 외부 간격
1. padding : 뷰의 내부 간격
1. layout_gravity : 정렬할 때 사용
1. background : 뷰의 배경 지정

# 6. Layout

1. 안드로이드 화면을 구성할 떄 뷰가 배치되는 모양을 결정하는 것을 Layout 이라고 부른다.
2. 안드로이드는 단말기 액정 사이즈와 해상도가 여러 종류가 있어 뷰가 배치될 위치를 결정하지 않고 배치될 형태를 결정하게 된다.
3. 개발자가 배치될 형태를 결정하게 되면 안드로이드 OS스스로가 단말기에 최적화된 사이즈와 위치를 결정하여 뷰를 배치한다.

### Linear Layout

1. 좌에서 우, 위에서 아래 방향으로 뷰를 배치하는 레이아웃
2. orientation: 뷰가 배칠될 방향
3. weight : Linear Layout에 배체된 뷰의 속성으로 배치 후 남은 공간을 할당 받을 비율을 설정한다.

### TextView

1. 사용자에게 텍스트를 보여줄 수 있는 뷰 입니다.
2. text : TextView를 통해 보여줄 문자열을 설정한다.
3. textAppearance : 미리 제공되는 테마를 설정한다.

### Button

1. 사용자가 누르면 개발자가 작성한 코드가 동작하는 뷰
2. OnClickListener : 사용자가 버튼을 눌렀을 때 반응하는 리스너
3. 람다식을 사용한 개발을 아주 좋아 합니다.

<pre>
<code>
package com.geoniljang.buttontutorial

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import kotlinx.android.synthetic.main.activity_main.\*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val listener1 = BtnListener()
        button.setOnClickListener(listener1)

        val listener2 = BtnListener2()
        button2.setOnClickListener(listener2)

        var listener3 = BtnLisnter3()
        button3.setOnClickListener(listener3)
        button4.setOnClickListener(listener3)

        button4.setOnClickListener { view -> textView.text = " 네 번째 버튼을 눌렀습니다." }
        button5.setOnClickListener { view -> textView.text = "다 섯 번쨰 버튼을 눌렀습니다." }

        val lisnter4 = View.OnClickListener { view ->
            when(view.id){
                R.id.button7 -> textView.text = "일곱번째 버튼을 눌렀습니다."
                R.id.button8 -> textView.text = "여덟번째 버튼을 눌렀습니다."
            }
        }
        button7.setOnClickListener (lisnter4)
        button8.setOnClickListener (lisnter4)


    }

    inner class BtnListener : View.OnClickListener {
        override fun onClick(v: View?) {
            textView.text = "첫 번째 버튼을 눌렀습니다."
        }
    }

    inner class BtnListener2 : View.OnClickListener {
        override fun onClick(v: View?) {
            textView.text = "두 번째 버튼을 눌렀습니다."
        }
    }

    inner class BtnLisnter3 : View.OnClickListener {
        override fun onClick(v: View?) {
            when (v?.id) {
                R.id.button3 -> {
                    textView.text = "세 번째 버튼을 눌렀습니다."
                }
                R.id.button4 -> {
                    textView.text = "네 번째 버튼을 눌렀습니다."
                }
            }
        }
    }


</code>
</pre>

### CheckBox

1. 항목을 제공하고 체크를 통해 선택할 수 있도록 하는 뷰
2. text : CheckBox에 표시되는 문자열을 설정한다.
3. checked : 체크상태를 표시 true or false
4. isCheck : 프로퍼티 체그 상태를 확인 할 수 있다.
5. toggle : !주요 메서드 - 현재 체크상태를 변경한다.

<pre>
<code>
package com.geoniljang.checkbox

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.CompoundButton
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        button.setOnClickListener { view ->
            textView.text = ""
            if (checkBox.isChecked == true) {
                textView.append("첫 번째 체크 박스 체크 되었습니다.\n")
            }
            if (checkBox2.isChecked == true) {
                textView.append("두 번째 체크 박스 체크 되었습니다. \n")
            }
            if (checkBox3.isChecked == true) {
                textView.append("세 번째 체크 박스 체크 되었습니다. \n")
            }
        }

        button2.setOnClickListener { view ->
            checkBox.isChecked = true
            checkBox2.isChecked = true
            checkBox3.isChecked = true
        }

        button3.setOnClickListener { view ->
            checkBox.isChecked = false
            checkBox2.isChecked = false
            checkBox3.isChecked = false
        }

        toggleButton.setOnClickListener { view ->
            checkBox3.toggle()
            checkBox.toggle()
            checkBox2.toggle()
        }

        val listener1 = CheckBoxListener()
        checkBox.setOnCheckedChangeListener(listener1)



        checkBox2.setOnCheckedChangeListener { target, isChecked ->
            if (isChecked) {
                textView.text = "이벤트 : 체크박스 2가 체크 되었습니다."
            } else {
                textView.text = "이벤트 : 체크박스 2가 체크 해제 되었습니다."
            }
        }

        checkBox3.setOnCheckedChangeListener{taget, isChecked ->
            if(isChecked){
                textView.text = "이벤트 : 체크 박스3이 체크 되었습니다."
            }else{
                textView.text = "이벤트 : 체크 박스3이 체크 해제되었습니다."
            }
        }

    }

    inner class CheckBoxListener : CompoundButton.OnCheckedChangeListener {
        override fun onCheckedChanged(buttonView: CompoundButton?, isChecked: Boolean) {
            if (isChecked == true) {
                textView.text = "이벤트 : 체크박스1이 체크되었습니다."
            } else {
                textView.text = "이벤트 : 체크박스1이 체크 해제 되었습니다."
            }
        }
    }

}

</code>
</pre>

### 라디오 버튼

1. 하나의 그룹 안에서 하나만 선택 할 수 있도록 하는 뷰
2. text: Radio Button에 표시되는 문자열을 설정한다.;
3. checked : 체크 상태를 설정한다. 라디오 버튼은 그룹 내에서 하나는 반드시 선택되어 있도록 제공하므로 반드시 하나는 체크를 해줘야 한다.
4. isChecked : Radio Button의 check상태 (true / false). 같은 그룹내 Radio Button 중 하나만 체크될 수 있다.
5. OnCheckedChangeListener : !주요 리스너 - 체크 상태가 변경되었을 때 반응하는 리스너

<pre>
<code>
package com.geoniljang.radiotutorial

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.RadioGroup
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        button.setOnClickListener { view ->
            when(group1.checkedRadioButtonId){
                R.id.radioButton -> textView.text = "라디오 1번 선택 되었습니다."
                R.id.radioButton2 -> textView.text = "라디오 2번 선택 되었습니다."
                R.id.radioButton3 -> textView.text = "라디오 3번 선택 되었습니다."
            }

            when(group2.checkedRadioButtonId){
                R.id.radioButton4 -> {textView3.text = "라이오 4번 선택 되었습니다."}
                R.id.radioButton5 -> {textView3.text = "라이오 6번 선택 되었습니다."}
                R.id.radioButton6 -> {textView3.text = "라이오 5번 선택 되었습니다."}

            }
        }

//        val listener = RadioListener()
//        group1.setOnCheckedChangeListener(listener)
//        group2.setOnCheckedChangeListener(listener)

        group1.setOnCheckedChangeListener{group: RadioGroup?, checkedId: Int ->
            when(checkedId){
                R.id.radioButton -> textView.text = "체크 이벤트 : 1 클릭"
                R.id.radioButton2 -> textView.text = "체크 이벤트 : 2 클릭"
                R.id.radioButton3 -> textView.text = "체크 이벤트 : 3 클릭"
            }
        }


    }

    inner class RadioListener: RadioGroup.OnCheckedChangeListener{
        override fun onCheckedChanged(group: RadioGroup?, checkedId: Int) {
            when(group?.id){
                R.id.group1 -> {
                    when(checkedId){
                        R.id.radioButton -> textView.text = "체크 이벤트 : 1 클릭"
                        R.id.radioButton2 -> textView.text = "체크 이벤트 : 2 클릭"
                        R.id.radioButton3 -> textView.text = "체크 이벤트 : 3 클릭"
                    }
                }
                R.id.group2 -> {
                    when(checkedId){
                        R.id.radioButton4 -> textView.text ="체크 이벤트 : 4클릭"
                        R.id.radioButton5 -> textView.text ="체크 이벤트 : 5클릭"
                        R.id.radioButton6 -> textView.text ="체크 이벤트 : 6클릭"
                    }
                }

            }
        }
    }
}

</code>
</pre>

### ProgressBar

1. 프로그램이 진행 되는 상황을 표현 하기위해서 사용합니다.
2. style : ProgressBar의 모양을 설정한다.
3. max : 최대 값
4. progress : 현재 값
5. max : 총 량
6. progress : 진행향
7. incrementProgressBy : 지정된 값 만큼 증가 혹은 감소 시킨다.

<pre>
<code>
package com.geoniljang.progressbar

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        button.setOnClickListener { view ->
            progressBar4.incrementProgressBy(5)
        }
        button2.setOnClickListener { view ->
            progressBar4.incrementProgressBy(-5)
        }

    }
}

</code>
</pre>

### SeekBar

1. ProgreeBar와 매우 유사하지만 사용자가 값을 직접 설정할 수 있는 기능을 갖추고 있다.
2. style : SeekBar의 모양을 설정한다.
3. max : 최대 값
4. progress : 현재 값
5. incrementProgressBy : 지정된 값 만큼 증가 혹은 감소시킨다
6. OnSeekBarChangeListener : SeekBar의 값이 변경되었 때 반응하는 리스너
7. 익명 중첩 클래스

<pre>
<code>
package com.geoniljang.progressbar

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        button.setOnClickListener { view ->
            progressBar4.incrementProgressBy(5)
        }
        button2.setOnClickListener { view ->
            progressBar4.incrementProgressBy(-5)
        }

    }
}

</code>
</pre>

### EditText

1. 사용자에게 문자열을 입력 받는 용도로 사용하는 뷰
2. inputType : 입력받을 데이터 타입을 선택 할 수 있다.
3. hint : 안내 문구를 설정한다.
4. text : 처음 보여질 때 나타날 문자열을 설정 한다.
5. imeOptions: 키보드 엔터키의 형태를 설정한다.
6. setText : EditText에 문자열을 설정한다.
7. OnEditorActionListener : 엔커 키를 누르면 반응하는 리스너
8. TextWatcher : 입력을 할 때 마다 반응하는 리스너.

<pre>
<code>
package com.geoniljang.edittext

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.text.Editable
import android.text.TextWatcher
import android.view.KeyEvent
import android.widget.TextView
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        button.setOnClickListener { view ->
            textView.text = editText.text
        }

        button3.setOnClickListener { view ->
            editText.setText("")
        }

//        val listener1 = EditorListener()
//        editText.setOnEditorActionListener(listener1)

        editText.setOnEditorActionListener { v, actionId, event ->
            println(v)
            textView.text = editText.text
            false
        }

//        val watcher = EditWatcher()
//        editText.addTextChangedListener(watcher)

        //익명 중첩 클래스
        editText.addTextChangedListener(object :TextWatcher{
            override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {

            }

            override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {
                textView.text = s
            }

            override fun afterTextChanged(s: Editable?) {

            }
        })

    }


//    inner class EditorListener: TextView.OnEditorActionListener{
//        override fun onEditorAction(v: TextView?, actionId: Int, event: KeyEvent?): Boolean {
//            textView.text = editText.text
//            return false
//        }
//    }

    inner class EditWatcher:TextWatcher{
        override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {

        }

        override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {
            textView.text = s
        }

        override fun afterTextChanged(s: Editable?) {

        }
    }

}

</code>
</pre>

### ImageView

1. src : 보여줄 이미지를 지정하는 속성
2. srcCompat : svg, 등 벡터 방식 이미지 사용시
3. 안드로이드에서 이미지를 넣는 폴더는 drawable 폴더이다.
4. 안드로이드 버전이 변경되면서
5. 안드로이드 버전이 변경되면서 mipmap 이라는 폴더를 제고하는데 이 폴더의 이미지는 비트맵이 아닌 벡터 방식으로 저장

# 코들린 문법

### 제어문

1. when

<pre>
<code>
    fun main(args: Arrays<String>){
        var value : Int = 3

        when(value){
            1 -> {
                println("Hello 1")
            }
            2 -> {
                println("Hello 2")
            }
            3 -> {
                println("Hello 3")
            }
            else -> println("Hello else")
        }
    }

    val value: Int = when(value ){
        1 -> 10
        2 -> 20
        3 -> 30
        else -> 100
    }

    val value2 : Boolean? = null

    when(value2){
        true ->{
            println(true)
        }
        false ->{
            println(false)
        }
        nukk ->{
            println("null!!!!")
        }
    }

    val value4 : Int = 10 
    when(value){
        is Int -> { // 자료형을 물어 보는 연산
            println("int")
        }
        else -> {

        }
    }

    in 60 ..[or until] 80 = 60이상 80 미만
    val a6 = Array(10, {0}) //lambda
    val a7 = Array(4, {1;2;4;2})
    
</code>
</pre>

### 배열

1. 배열이 필요한 이유?
   - 어떠한 그룹이 필요할 때

<pre>
<code>
    fun main(array: Array<String>){
        val one : Int = 1
        val two : Int = 2
        val three : Int = 3

        //1 번째 방법 = 선언과 초기화를 같이
        var group1 = arrayOf<Int>(1,2,3,4,5)
        println(group1 is Array)
 

        group1.get(index) 
        group1[index]

        group1.set(index, value)
        group1[index] = value

    }
    
    val a1 = intArraOf(1,2,3,12,3);

    val aInt = intArrayOf(1,2,3,1)
    val aChar = charArrayOf('a','b')
    val aDouble = doubleArrayOf(2.3, 123.23,424.42)


</code>
</pre>

### Collection

1. list
2. set
3. map

<pre>
<code>
    fun main(agrs: Array<String>){

        << Imutable 변경불가능 >> 
        // List
        val numberList = listOf<Int>(1,2,3,2,3)
        println(numberList)// 1,2,3,2,3 -> 중봅을 허용한다.
        println(numberList.get(0))
        println(numberList[0])


        val numberList1 = mutableListOf<Int>(1,2,3)


        << Imutable 변경불가능 >>
        // Set 
        val numberSet = setOf<Int>(1,2,3,1,3,)
        println(numberSet) // 1,2,3 -> 중복을 허용하지 않는다.
        numberSet.forEach{it
            println(it)
        }

        val numberSet1 = mutableSetOf<Int>(1,2,3)


        << Imutable 변경불가능 >>
        // Map -> Key, Value 방식으로 관리한다.
        val numberMap = mapOf<String, Int>("one" to 1, "two" to 2)

        val numberMap1 = mutableMapOf<Int>("one" to 1, "two" to 2)
        numberMap1.put("three", 3)


    }
</code>
</pre>
