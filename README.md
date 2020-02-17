# Basic Android

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
