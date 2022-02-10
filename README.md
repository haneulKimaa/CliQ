# CliQ - 성교육 퀴즈
### 퀴즈로 배우는 우리들의 언어
---
### 1.  개발 목표
+ 서울여자대학교 바롬 인성교육 프로젝트3의 일환으로, 그 주제인 '여성, 젠더, 사회'의 문제를 해결할 수 있는 성교육 퀴즈 어플리케이션을 제작한다.
+ Front-end 개발 실력을 향상시킨다.
+ 디자이너와 협업한다.
+ 어플리케이션을 App store에 출시한다.  


### 2.  개발 언어
+ Swift 


### 3.  개발 툴
+ Xcode 

### 4.  최적화 디바이스
+ iPhone XR/XS Max/11/11 Pro Max  


### 5.  주요 기능
+ 도입부 scroll view
+ 플레이화면 - 글자 선택시 정답인지 확인
+ 플레이화면 - 힌트 버튼 클릭시 정답을 제외한 글자 랜덤하게 삭제
+ 레벨에 따른 문제 설정
+ 전체 문제 정답 확인 (= 정보 모아보기)


### 6.  스크린샷
<img src="https://user-images.githubusercontent.com/63438947/129935690-4cf26d02-b20c-418f-a48e-552fb7d0d0ce.png" width="30%">  <img src="https://user-images.githubusercontent.com/63438947/129935703-61363168-b4de-469c-bf63-9ea362ccba82.png" width="30%">  <img src="https://user-images.githubusercontent.com/63438947/129935707-c5ab38bc-29d2-4732-9871-f325a69993f5.png" width="30%">  <img src="https://user-images.githubusercontent.com/63438947/129935710-323990ca-8e23-41ba-ae29-801193230b14.png" width="30%">  <img src="https://user-images.githubusercontent.com/63438947/129935712-50962ff9-d333-4276-91a1-34bfee57b72a.png" width="30%">  



### 7.  개발 사항 (개인)
+ 글자 클릭시 정답인지 확인


  1. 글자수가 같은 문제를 묶고
  2. 각 글자 자리수 각각 이미 입력되었는지 확인 후
  3. 정답 판정 및 다음 문제로 넘기기
```Swift
else if quizCount == 1 || quizCount == 2 || quizCount == 3 || quizCount == 4 || quizCount == 5 || quizCount == 6 || quizCount == 7 || quizCount == 8 || quizCount == 9 || quizCount == 10 || quizCount == 11 || quizCount == 19 {
            if isFirstSelected == false && isSecondSelected == false {
                answer2_1.text = sender.titleLabel?.text
                isFirstSelected = true
                clickedAnswerLabel.text = answer2_1.text
            }
            else if isFirstSelected == true && isSecondSelected == false{
                answer2_2.text = sender.titleLabel?.text
                isSecondSelected = true
                clickedAnswerLabel.text =  answer2_1.text! + answer2_2.text!
                if clickedAnswerLabel.text == correctAnswer{
                    UserDefaults.standard.setValue(10, forKey: "temp")
                    correctAnswerImage.isHidden = false
                    let ViewControllerInfo = self.storyboard?.instantiateViewController(withIdentifier: "Info")
                    var temp = UserDefaults.standard.integer(forKey: "Level")
                    temp += 1
                    UserDefaults.standard.setValue(temp, forKey: "Level")
                    self.navigationController?.pushViewController(ViewControllerInfo!, animated: true)
                }
                else {
                    wrongAnswerImage.isHidden = false
                    UIView.animate(withDuration: 0.8, delay: 0.1,
                                   options: UIView.AnimationOptions.curveEaseOut, animations: ({
                                    self.wrongAnswerImage.transform = CGAffineTransform(scaleX: 3.0, y: 3.0)
                                    self.wrongAnswerImage.alpha = 1;
                                   }),completion: nil)
                    UIView.animate(withDuration: 0.8, delay: 0.5, animations: ({
                        self.wrongAnswerImage.alpha = 0;
                    }))
                    self.wrongAnswerImage.transform = CGAffineTransform(scaleX: 1.5, y: 1.5)
                    isFirstSelected = false
                    isSecondSelected = false
                    clickedAnswerLabel.text = ""
                    
                    answer2_1.text = ""
                    answer2_2.text = ""
                    for i in 0...11{
                        btnChar[i].isUserInteractionEnabled = true
                        btnChar[i].setTitleColor(.black, for: .normal)
                    }
                }
            }
        }
```
+ 힌트 버튼 클릭시 정답이 아닌 글자 중 세 글자 삭제


  1. 해당 단어의 각각의 글자와 아래 글자가 같은지 판단하여 
  2. 같지 않은 글자 중 랜덤한 세 글자를 보이지 않게 처리

```Swift
if clickedNumber != 2{
            var spilitCorrectAnswer: Array<Character> =  []
            
            spilitCorrectAnswer = Array(correctAnswer)
            print(spilitCorrectAnswer)
            
            for i in 0..<correctAnswer.count{
                for j in 0..<btnChar.count{
                    print("1")
                    if btnChar[j].titleLabel?.text == "\(spilitCorrectAnswer[i])" {
                    }
                    else{
                        isAddNotCorrectAnswer[j] += 1
                    }
                }
            }
            for j in 0..<btnChar.count{
                if isAddNotCorrectAnswer[j] == correctAnswer.count{
                    print("add")
                    hideArrayHint.append(btnChar[j])
                }
                else{}
            }
                hideArrayHint.shuffle()
                hideArrayHint[0].isHidden = true
                hideArrayHint[1].isHidden = true
                hideArrayHint[2].isHidden = true
        }
```


### 8.  App store 등록 기간
+ 2020.6.5 ~ 2021.6.5

<img src="https://user-images.githubusercontent.com/63438947/129935496-514b8da9-9d6c-438d-b7cf-ee976d3eaa3e.png" width="30%">  <img src="https://user-images.githubusercontent.com/63438947/129935596-9fd3c0ad-6475-4e29-bd05-7f497d32a9df.png" width="30%">



