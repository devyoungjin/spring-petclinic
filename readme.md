백기선님의 [예제로 배우는 스프링 입문] 강의를 듣다가 다 듣지못한 적이 있는데, 이번에 다시 듣게되었다. 듣는김에 정리하면 좋을것 같아 정리하면서 작성해보는 글.

[스프링 샘플 웹 애플리케이션](https://github.com/spring-projects/spring-petclinic)을 다뤄보면서 스프링의 IoC, AOP, PSA 등에 대해 예제코드를 통해 맛보는 과정이다.

본 과정은 아래의 조건에 대한 선수학습을 요구한다.

1. 자바 프로그래밍 기초
2. IDE (Intelli J 또는 Eclipse)
3. 빌드 툴 (Gradle 또는 메이븐)
4. Git



## ToC

- 프로젝트 설정
  - [Clone a sample project](#clone)
  - [Build and run a project](#build-run)
- 프로젝트 살펴보기
  - [프로젝트 살펴보기](#explore)
- 프로젝트 과제
  - [과제](#quiz)
  - [풀이](#solution)

<br>

## <a name="clone">Clone a sample project</a>

먼저 샘플 애플리케이션을 원격저장소에서 클론해서 가져와야 한다. 필자의 경우는 개인 원격저장소로 fork한 이후 clone했다.

원격 저장소의 URI부터 가져오자.

<img src="https://lh3.googleusercontent.com/ov5vKj6r3uJYRU1PAF_Xf_oauZKkRtx5mgWbbte382yTnANwL5mzn5EEBZjyRdITm2crxTtQICW5x4DNht4rC0OFvVvm62um6YhUkfaYsU9C6mI4BkQGUKdzxqWE7dhgEhjPJmFr0y_n76HvyFcr9IZN_UaJqtoJxGpVxCVrVkilWewvBebIw_6V3D3VWtGOKjIl70Upd5jM-GKjhQfcSoyVATyhLzXNTUvzkJd_SvRN4rfN-_s9nZ_8u_jQVk4bOXri33Q9iUrrlf5VrL_2Jh_MbC6cZn8qTIFnsOpRslP8B6aVXG3qjzDe4TgROfNEHz0hm8IMMgLRFMMfXjdpKfqM4Zp2GhGY5dO34ak6iNaEy30ubSGJ3Yrk57J1cBfriVRXiY8cLeplhQfVqiTbPbkcKYY5fnYJEJJPu_snsU4jxzLHx0nfLfyWiRJer4mRYK1ZwGlAfd8nhLK0Y19NhTlWHXbxAOvidYQSltCfL9Wv5DufCtWY4vk0t8p_LWfiFUYnhPFSKuXSJNWaghOU9fXJn46K0VhxYg_SOQqKbuubCKTpD4xaMp9POpvMfGd8cI2uqL8IfPYCZQnYhnSGTAaZOU01jxR0YA22lOFyEd3HDHs1Vh3Du1S6MzkoluGppeRFqusT_ljcXaDPZMCFi812oUoOq8znjjZ99CuebPMGH2j7RSfpZvGekqkOXMc=w987-h592-no" style="zoom:50%;" />



이후에 Intelli J를 열어서 **[Get from Version Control]** 버튼을 클릭하여 아까 클립보드에 복사해둔 원격저장소 URI를 붙여넣어서 가져오자.

![](https://lh3.googleusercontent.com/g40Xf_ZeVVaKzDqAIPPuaQXnGHSj8AsG61l4fiJrme7T1dlAUCJDxnENX1a5SWSpXS3MJgjo4SiYG3EYo6nkyTcJEu83aCwPrQgPBkCj6beFsOZDy5A86rYrXu5HKMKWQ5KM3piuZiLNyz-yWN5aCpe-wwu9kwDI-G59B8fNTaHePWP0v76J_vWaMi3mEvARpLSEZurf7ZK6fn_8Ovl_PGfW747kuzzXMgJ7Jhy4FTT_15MjKDZnyZGmPA2m2KFBJTqGWqLYsXGi_yc2KE2akAc_EYXn7meFvbBor4WMZvIFgNEEA2gNl0oZu05a6SJq7XhzFfe-c4EO6tRGESjoJQLyhqzNCBugGDDNgC1IF6QaRXWSP5GUzWDDw5RLfj71_8_p4xFMqMdqIWkM5_Z3ZBks2Ae2jfL0cXYss0JUpz5wutMtAcYvg0pMDEzMgPMmnTtJlAKVBOsSY8Z-GoWxJ8ZrokwidcFSbxPvd81SxqyRtXbveGH53HxM8c06JmjkuToxDow4_pAXN8GgNnMjcbFtF70ZsoNU5GWb0CMtmKSXTYfdpFlCh301rxhv22rOazKuIjxjBcyMMsAAUW2ROTV7enUlNuIbfBFnb7nVj_q11xWxPFtpftYN2Nunv8JbIv19egBS7WCFISh41cmuCP_9t36k3q6-9QQbGgCAgaeb5GzMc6-ZMeV4iJ8Dv2BbAl2cb-C_shgbvPhlSBRLFI5RUX15mtXpH0-c54mQx_xpWQQdw4QBryDz=w500-h305-no)

<br>

본 샘플 애플리케이션의 빌드 툴은 메이븐이 설정되어 있다. 메이븐의 설정파일 pom.xml을 확인해보면, 따로 `<packaging>`이 설정되어 있지 않은데, 이렇게 따로 `<packaging>`설정이 없으면 이 프로젝트는 jar 프로젝트라고 한다. jar은 Java Application Archive의 약자라고 한다. 타입으로는 war(Web Application Archive)가 있다.



**jar와 war의 차이**

jar는 하나의 java application 기능을 가능하도록 하는 압축파일이며, 자바 클래스 파일들이 주로 압축대상에 해당한다.

war는 jar와 달리 웹 어플리케이션을 지원하기 위한 압축방식인데, jar보다 더 큰 범위의 압축파일이다. 웹 애플리케이션에 필요한 모든 자원(jsp, servlet, gif, html, jar)을 포함한다.

<br>

## <a name="build-run">Build and run a project</a>

당연히 작동되겠지만, 해당 프로젝트가 잘 빌드되고, 작동되는지 알아보자.

**메이븐 빌드하기**

~~~
./mvnw package
~~~

[![asciicast](https://asciinema.org/a/rCuwrlPLzK7FbojYLvqfjGzC4.svg)](https://asciinema.org/a/rCuwrlPLzK7FbojYLvqfjGzC4)

위의 화면처럼 화면 마지막에 <span style="color: green;">**BUILD SUCCESS**</span>가 출력되었다면, 성공적으로 빌드가 된 것이다.

이제 메이븐으로 빌드한 jar파일을 Tomcat(웹 서버)으로 실행해볼 것이다. 

~~~
java -jar target/*jar
~~~

[![asciicast](https://asciinema.org/a/HNNbEegr9IRlpJlydEAfaImOj.svg)](https://asciinema.org/a/HNNbEegr9IRlpJlydEAfaImOj)

<span style="color: green;">**Started PetClinincApplication**</span>이라는 메세지가 마지막에 출력되었다면 성공적으로 실행된 것이다.

로컬호스트에서 정상적으로 프로젝트가 구동되는것을 확인할 수 있다.

![](https://lh3.googleusercontent.com/pT4QlA65nQbcrhP8QvItBOWCRdvfNRXQEnbDy_AUpniXaBFE86V_eK34tJABlMqTCJBSguvolsFfSnvvi5c_GREjUPb2hxmrqLT68yXBFAFD22EZhXQHFZJhrNtdbQGHZVSvNZqDDRBWj2VTZ7f8iYgrSpHZOStNtXhcA3UZUvW7VtaoVV1XVq1KckyI5pFvYpc4F66C7IgISQcuLLOW2FZUSBrULPmyn_EtK3uPuyzkKtlGrgzD7PRp9o8_ipfXjtZkhUJW94Z2ElcJy8e2jnPzLFhhub4PGU111-wXqsAaEWwROtNEzHY7MynutF3VLbpik2HpnMDtniG4l051oJB5EchUSea0qqA5H1ZeQejTXXe2yqLLKhMyt8JG6GGODzCC3dVeikEjWZ4BIUukrQVtOoF5_KsicfL5uVNK1lWcClwja6SgW4MVCXwF4IsfEIEPLeRlYmnwQGxtUcSfeROPKeVwq2wBonT4ihB5bPliyruwt9EWU3b5PF5H2MdDJBwUDtdgWf1d2qYPEyPQaLZSJHZam5e8SAjp3fUwGVe3aRXH4sSiYkORp8Xw3nbQ9UHFx6rMP3Q_mcQ-wvr1puWtrZ_JKHSR3jb9yN0b5Na1PMx5RbrpQ89lh8kR_xnXbdRk4T_eCB-24rRnpubzDQwW4KsPqO00OrUEimPAGuscKREC6sr2n8kz4v1hkginOx85h67dklGvZZ46m49FJtIjOcB_qzQL_xGlz83MBBfB48apa3D5dSyA=w1440-h922-no)

<br>

## <a name="explore">프로젝트 살펴보기</a>

프로젝트가 어떻게 작동되는 건지 조금 더 자세히 살펴보기 위해 application.properties의 debug모드를 활성화시키겠다.

~~~
loggin.level.org.springframework.web=DEBUG
~~~

![](https://lh3.googleusercontent.com/Y08n5Camz7tShU4Nmp90MzIhC6TqFQzcwCBWmHI3hxkiTGR4XIfd6tqjnv1-ImB8eD0iSNSfFkOO3LPkzljrF1hTYXisF77rMJQk3R1IfZOcJ5jbRaS7f_VnHb3MBq_YqfrL4VGsyO3ScQw3PMCFNemMkbXTmdS7aIIoPiinEm4istEwHwI2iOgvWj8orZgKHvT0jYt54_TLEK20i_6_MqmtawMFoB9Q1UJEani-VjflmTIZBWyqT1EhtMKgnZAdRgo6MO7i-jfJbTtfgiXO4kvQC4Y_8VUxanT2V0Jm_dYKyRn3M46zQxdNyEFfSzpth4ph6c8-WTXdzCEBF4KCPOLlOpt8j3PTXr3mYx9YVosButw1ltSjcmUjJQeKmuPyC9bwkKZCB-ZRFIyJzAGoOTgRr4qE73wZ5w0g8ClhghTSJPGXP8mu6PzxSysHtDud9436IfXcAIdrC7CvvSNNCNTKhLoRMy3uWsXTuyyljwB39WdnT3pe8quFhUQLmf36L2t-Sm4gSQQtowhzHFVxmtrkKb_r0RMjz3FaOYWQLtV_ZGI2TMb4Kk_ASujaff1fm2b7EMCfUOjHr0dofYctXIaJOZXe4ncWYEnkyolTJS5czhMlvYfA0WW5bf0P1bG_YI6MyGsW7gNp5WORQSPEn9XuI7bwsVAcOuwxwCUMWhaaspkPrmS9OTSc19mRz3ikRTA38IFldHk6bAlYRpuPhyNfA0fRjLpQIxrfQLB-ZDrUzIPuM0iDjv_b=w1310-h798-no)

주석처리되어있는 문장을 주석해제 처리하고 다시 빌드하고, 웹 서버를 구동해보자.



웹서버를 구동시킨 이후, **FIND OWNERS**를 시도해보았다.

![](https://lh3.googleusercontent.com/bCzHXxE4Ml2Cj0KD0-myn9If1YddnT3QftxEPPoQyH0r1EhVq3q66UMfqSWftUOy4WmaUqgN77uyqDT3FfRgle4yw1HvQ7x5ZxKPHRTBEdAO0QPI_YYo0qo5_3eKHstKuMWfmDd83lgHEBAiVna0EtD4yJYoZ07fQ1E05SnQkTu2TEOR5gn0083a8ERnNUMEirar5yb5ylXRCaVgvEigGAfa3wJerfEOY8yWzQSE90R8ZmQbv88z2V4ySLyi1RozYWxFZcrUE1YZqLpg6k0SOTlqTgkWGcAKsFkixV1t3mNEmKu0f3kQ6RPVRqZuwRPIDvxDDIOiMLAJDd5cln8kY0PPsqlNNZTJ7ijno2bxh3gjaubCpXPBgFl6e_uxxFJ-H8uhBFTvz1HT5BcxB_4LvHoszW6mNssDIU4zIFcrbQei9sBBTg1oH2KWDZjTM8auzHpYMrRnfaONryY0r651SXRhpbbrnLvarsccGbk_7pQzA9jlL5sbaw7tffFG7xeEB-go57DI6cfeO5SXgdmfOt2VDoAAfUwSMRaOGveLJXcoHH7ZLa_Z0d7OcFu8CeXW7twJJZsbo4iN6b_o-uXZF8YLFRsnxImFkNMU_QzqWSl49rU48ta9_8iAWb8BUDgMOTY6FWf9MK6KVlB4w_cjwMK1dPf0JzEQOMPnm5xvKj5DlwS0qrKqmZ7yO4alYZm_CDvjSwML5tHJqn-sovCLGROv7CP1nPAwPwkWOQNnAV-TIsmEmOcbr1X5=w2108-h728-no)

이렇게 했을때 콘솔에서는 어떤 일이 벌어질까

![](https://lh3.googleusercontent.com/vY55SrvtFWHWImz0U7NSoquoovUjo7r-1m6ZTTuFFTSkCXHcr9mUdaCTh7_pzuOdlOy0VVr3vdEAi8EROm0FpfXpSs18E5RTW1-X3rRZTwzyhV0QlsFL0ggSDUoEuL0yX8T7XZKTVkdhwwhE4tJZO_hruMyNNxV3tFr5ean8e-511xZq3Y__3RD1ZMfECfMfYwjyL8M6O9VD1TBbeqdgMoFjaw4HN1PBKyDvAsbHqDUslWn7tBtx300jW7pyOHlsB57CXUAP24pOB0yK1OO22ZhrCu1KnpIYMLcLt3_UpeBRTrXJoa0IL-olgGEcCAzqqntyORCMWTipPVM1q-Kzs1khS-E4UnJdxq1X-JJhGSC789drj1_vJQF9zq_ksi36VcS00tgDdmN_XTyMxUHdHgN3J05B1pkSI5qkhJfQHi6bw83HyZqT74fw7gf3modyIxSne-65qMhlYaqB2aNnR9PRMqYjDAm1eUMq7ef0Txp8hftxTqjZJMbGV1D0dJUmGZQPv8mhLW74Lgup-9eq6WMBTG5tihgKzNndF8wQ2UOAldE1CNEy4Yyg3DVIQn0vsQQuuORnWPi5E2MoMH6hBs_8yr8V4z5zSmtg_aoF11u_Bslte2V-PwNHQLz0-ya3a9visWP1S_OxXmJgXGMphL7NOkz0jYEupLGOH1ZEZe8dREeOkJCattGpWFgSE_EOWlTI85K0KVEbtiLANbPIagjZRQu3IUKovpCY-2esAGv_TMQMYezoQPiT=w2106-h746-no)

`/owners/find` 라는 URI를 맵핑하는 GET 요청이 들어왔음을 알 수 있다.

두번째 출력된 로그에서는 어떤 컨트롤러(`org.springframework.samples.petclinic.owner.OwnerController`)의 어떤 메서드(`initFindForm`)가 작동되었는지도 알 수 있다.

마지막 출력된 문장에서는 200 OK가 출력되었는데, 리소스를 성공적으로 불러왔음을 나타내는 HTTP 상태코드인것 같다.

<br>

## <a name="quiz">과제</a>

- Find Owner에서 LastName 대신 FirstName으로 조회하기
- 단어가 정확히 일치하지 않아도 일부 일치해도 결과 출력하기
- Owner 객체에 age 추가하기

<br>

## <a name="solution">풀이</a>

### **Find Owner에서 LastName대신 FirstName으로 조회하기**

![](https://lh3.googleusercontent.com/jRJd10fZSgBIyehquyjIEE9HGcGeNnJbOqCtdczJy3buXgAcSeUAY4xZ4AzO5D6f5p1ExUpieH63kuQQbwXEz9tyHUMfmEUBKoGd3OzWLk1BVwrPwV4lChxD9fHGqJTjaqhKkI3zbPee-EBJ65Zrrh9um1sQ1xVjJRf9ASXPmDXPbUnLkbqCZL7uM7nD82LnL5jNPqp-HujNSSI4R9yyvZsuOKh0UYheFj5Dbxj9PnjcPHWX2dgMpBwsE61mV1R8n-F1dpf7gfiy9B_KryFHqarHN1QaZHs6aSXjum9HEU0MefO2tNdEsAMJ76bcmDNzv7LBOwKwAQFH4M_G60Eq4--QKSYoiaXeYlIWAq4eQwlpLGL0DS5ZJ4uRmmfYTUcymyo6NoUPaRNRXxBLhvGiyo9cjLz7WHkf76mc8jM5ltHn_WBzU0odBHLktHVWthQaGg6NbSMcX5cKV9CJa7p4GSWmso4k2Xj6WX66n0vL-viC_-ZXvooUMgCOuU4NWhGUSwCAa_djIKfLM2V3cpyUboqjlOIieCXreywVmkgzrymT5F8DimyXhS3UpZ6PuLRnL_NHzE0SJUcMwmf1303bMoWsaGizq9NRm80duA8BtBapTkmOh73GAy5cpw2XclQNzIAu-dH77jXvgsxjkYBtw57E34YRJytSgYptMEuFiWLmFRghEL_xZUaGEqJ9v1t6nKLcfggka4k9ITialNWMNE8ITNRPWTkuIq1QU9I779r_N_QdU1VZebQ_=w640-h530-no)

`/owners/find` 에서 조회 기준으로 Last name으로 되어있는데 이 텍스트부터 바꾸는것으로 시작한다.

**findOwners.html**

~~~html
<h2>Find Owners</h2>

<form th:object="${owner}" th:action="@{/owners}" method="get"
      class="form-horizontal" id="search-owner-form">
  <div class="form-group">
    <div class="control-group" id="lastNameGroup">
      <label class="col-sm-2 control-label">First name </label>
      <div class="col-sm-10">
        <input class="form-control" th:field="*{firstName}" size="30"
               maxlength="80" /> 
        <span class="help-inline">
          <div th:if="${#fields.hasAnyErrors()}">
            <p th:each="err : ${#fields.allErrors()}" th:text="${err}">
              Error
            </p>
          </div>
        </span>
      </div>
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
      <button type="submit" class="btn btn-default">Find
        Owner</button>
    </div>
  </div>

</form>
~~~

전체 코드를 가져오긴 했지만, `label`과 입력받은 데이터를 바인딩처리할 `input` 박스의 `th:field` 값만 바꿔주었다. 이제 입력받은 값을 lastName이 아니라 firstName으로 인식할 수 있게 되었다. 이제 이렇게 가져온 데이터를 처리할 컨트롤러를 수정할 차례이다.



**OwnerController.java**

~~~java
@GetMapping("/owners")
public String processFindForm(Owner owner, BindingResult result, Map<String, Object> model) {

  // allow parameterless GET request for /owners to return all records
  if (owner.getFirstName() == null) {
    owner.setFirstName(""); // empty string signifies broadest possible search
  }
  
  // find owners by last name
  Collection<Owner> results = this.owners.findByFirstName(owner.getFirstName());
  if (results.isEmpty()) {
    // no owners found
    result.rejectValue("firstName", "notFound", "not found");
    return "owners/findOwners";
  } 
  ...
}
~~~

OwnerController의 `processFindForm` 메서드를 보면, 입력받은 lastName이 null일 경우, LastName을 빈 값(`""`)으로 지정하도록 되어있다. 여기서 `lastName`을 모두 `firstName`으로 바꿔준다. 

아래 `<Owner>` 컬렉션을 선언하는 코드에서도 `this.owners.findByLastName()`을 `this.owners.findByFirstName()`으로 바꿔주어야 한다. 단, 이 때 `findByFirstName()`은 OwnerRepository에 추가되어 있어야 한다.

**OwnerRepository**

~~~java
/**
  * Retrieve {@link Owner}s from the data store by first name, returning all owners
  * whose last name <i>starts</i> with the given name.
  * @param firstName Value to search for
  * @return a Collection of matching {@link Owner}s (or an empty Collection if none
  * found)
*/
@Query("SELECT DISTINCT owner FROM Owner owner left join fetch owner.pets WHERE owner.firstName LIKE :firstName%")
@Transactional(readOnly = true)
Collection<Owner> findByFirstName(@Param("firstName") String firstName);
~~~

`findByLastName`을 그대로 복사해서 `findByFirstName`이라는 컬렉션으로 새로 선언해준다. 파라미터값도 `lastName`대신 `firstName`으로 바꿔준다. 

이렇게 `findByLastName`을 생성했으면, 컨트롤러에서 사용할 수 있게 된다. 

컨트롤러가 완성되면, `owner`객체의 `getFirstName()`을 통해 불러온 firstName을, ownerRepository에서 생성한 Owner 컬렉션타입의 `findByFirstName`객체에 담고, 최종적으로 Owner 컬렉션타입의 `result` 객체에 담아냄으로써 이를 findOwner.html에서 출력하는 것이다.

<br>



