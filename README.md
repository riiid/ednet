# EdNet

> Paper : https://arxiv.org/abs/1912.03072

> Leaderboard : [Link](http://ednet-leaderboard.s3-website-ap-northeast-1.amazonaws.com/)

*EdNet* is the dataset of all student-system interactions collected over 2 years by *Santa*, a multi-platform AI tutoring service with more than 780K users in Korea available through Android, iOS and web.



## Properties of EdNet
EdNet dataset contains various features of student actions such as which learning material he have consumed, response, how much time he have spent for solving a given question or reading through expert’s commentary. And EdNet have some properties which is introduced following.

### 1. Large scale
EdNet is composed of a total of 131,441,538 interactions  collected from 784,309 students of *Santa* since 2017. Each student has generated 441.20 interactions while using *Santa* on average. EdNet, based on those interactions, makes researchers possible to access to a large-scale real-world ITS data. Moreover, *Santa* provides a total 13,169 problems and 1,021 lectures tagged with 293 types of skills, and each of them has been consumed 95,294,926 times and 601,805 times, respectively. To the best of our knowledge, this is the largest dataset in education available to the public in terms of the total number of students, interactions, and interaction types.


### 2. Diversity
EdNet offers the most diverse set of interactions among all existing ITS data. The set of behaviors directly related to learning is also richer than other datasets, as EdNet includes learning activities such as reading explanations and watching lectures not provided by others. Such diversity enables researchers to analyze students from various perspectives. For example, purchasing logs may help to analyze student's engagement for learning. Also, contents information table is provided separately.

### 3. Hierarchy
EdNet has a hierarchical structure of different data points. To provide various kinds of actions in a consistent and organized manner, EdNet offers the datasets in four different levels each named KT1, KT2, KT3 and KT4. As the level of the dataset increases, the number of actions and types of actions involved also increase. The details and descriptions of each dataset is described below. 

### 4. Multi-platform
In the age where students have access to various devices spanning from personal computers to smartphones and AI speakers, it is inevitable for ITSs to offer the access from multiple platforms.  Accordingly, *Santa* is a multi-platform system available in iOS, Android and Web and EdNet contains data points gathered from both mobile and desktop.This allows the study of AIEd models suited for future multi-platform ITSs, utilizing the data collected from different platforms in a consistent manner.

## Dataset
As we said, there are four datasets named KT1, KT2, KT3, and KT4 with different extents. Here's common features of these datasets:
* The whole dataset is divided by students: `{user_id}.csv` only contains `{user_id}`'s interactions. 
* The timestamps are different from the real values, which are modified (shifted by fixed values) due to security issues.
### Download links
- EdNet-KT1 : [bit.ly/ednet_kt1](http://bit.ly/ednet_kt1)
- EdNet-KT2 : [bit.ly/ednet-kt2](http://bit.ly/ednet-kt2)
- EdNet-KT3 : [bit.ly/ednet-kt3](http://bit.ly/ednet-kt3)
- EdNet-KT4 : [bit.ly/ednet-kt4](http://bit.ly/ednet-kt4)
- Contents : [bit.ly/ednet-content](http://bit.ly/ednet-content)

### KT1
> Download a `.zip` file from [bit.ly/ednet_kt1](http://bit.ly/ednet_kt1)

|Specification| |
|----|---|
| Size of the compressed file | 1.2GB |
| Size of the uncompressed file | 5.6GB |
| The number of files | 784,309 |

#### Structure
KT1 consists of students' question-solving logs, which is the most basic and fundamental information that can be used  by various deep-learning knowledge tracing models such as Deep Knowledge Tracing  and Self-Attentive Knowledge Tracing. EdNet-KT1 is the record of *Santa* collected since Apr 18. 2017 following this question-response sequence format. 
A major property of EdNet is that the questions come in *bundles*. That is, a collection of questions sharing a common passage, picture or listening material. For example, questions of ID `q2319`, `q2320` and `q2321` may share the same reading passage. In this case, the questions are said to form a bundle and will be given to the student with corresponding shared material. When a bundle is given, a student have access to all the problems and has to respond all of them in order to complete the bundle. 

#### Description
* `timestamp` is the moment the question was given, represented as **Unix timestamp in milliseconds**.
* `solving_id` represents each learning session of students corresponds to each bunle. It is a form of single **integer**, starting from `1`. 
* `question_id` is the ID of the question that given to student, which is a form of `q{integer}`.
* `user_answer` is the answer that the student submitted, recorded as a character between `a` and `d` inclusively. 
* `elapsed_time` is the time that the students spends on each question in **milliseconds**.
#### Example

| timestamp     | question\_id | bundle\_id | user\_answer | elapsed\_time |
|---------------|--------------|------------|--------------|---------------|
|1548996377530 | 48       | q2844       | d           |47000        |
|1548996378149 | 48        | q2845       | d            | 47000          |
|1548996378665 | 48         | q2846      | d            |  47000         |
|1548996671661 | 49        | q4353      | c            | 67000       |
|1548996787866 | 50        | q3944      | a            | 54000        |

### KT2
> Download a `.zip` file from [bit.ly/ednet-kt2](http://bit.ly/ednet-kt2)

|Specification| |
|----|---|
| Size of the compressed file | 0.6GB(555.8MB) |
| Size of the uncompressed file | 3.1GB |
| The number of files | 297,444 |

#### Structure

A major drawback of the question-response sequence format is that it cannot account for the inherent heterogeneity of students' actions.  For example, a student may alternately select one of two answer choices before submitting his final answer, which possibly signals that he is unsure of either of the options. Due to the restriction of question-response format, a dataset following such format like EdNet-KT1 can't effectively represent such situation. To overcome this limitation, *Santa* have collected the full behavior of students since Aug. 27, 2018. As a result, the datasets EdNet-KT2, EdNet-KT3 and EdNet-KT4 of *action sequences* of each user are compiled. Each *action* represents a single unit of behavior made by a student in the *Santa* UI, such as watching a video lecture, choosing a response option, or reading a passage. By recording a student's behavior as-is, the datasets represent each student's behavior more accurately and allows AIEd models to incorporate finer details of learning history. EdNet-KT2, the simplest action-based dataset of EdNet, consists of the actions related to question-solving activities. Note that the features of KT1 can be fully recovered by the columns of KT2, and KT2 contains further information such as the study mode of student or the intermediate responses provided by student.


#### Description

* `action_type` is one of the following: `enter`, `respond`, and `submit`. 
    *  `enter` is recorded when student first receives and views a question bundle through UI.
    *  `respond` is recorded when the student selects an answer choice to one of the questions in the bundle. A student can respond to the same question multiple times. In this case, only the last response before submitting his final answer is considered as his response.
    * `submit` is recorded when the student submits his final answers to the the given bundle.
*  `item_id` is The ID of item involved with the action. For EdNet-KT2, only the IDs of questions and bundles are recorded. A bundle is assigned for actions of type `enter` and `submit`.
* `source` shows *where* the student solve a question or watch a lecture in *Santa* UI. There are several sources in *Santa* that students can solve questions or watch lectures. For KT2, only the sources that provides question-solving environments are recorded.
    * In ``sprint``, students choose a part that they want to study. After that, they can only solve questions belongs to the part that they choose, until they change to different part or select different source. 
    *  For each day, *Santa* recommends questions and lectures based on each student's current knowledge status, i.e. correctness probabilities predicted by the Collaborative Filtering model. Such source is called *Today's Recommendation*. Questions that belong to particular parts can be recommended, ``todays_recommendation::sprint``, ``todays_recommendation::review_quiz``
    * Once the number of incorrect answers to questions with particular tags exceeds certain threshold, *Santa* suggests  lectures and questions with corresponding tags. Such suggestion is recorded as `adaptive_offer`. It also offers lectures and questions if the average correctness rate of questions with particular tags decreased by more than a certain threshold. 

    * *All Parts* is a source that students solve questions that *Santa* recommends following a certain algorithm, from all possible candidates. This is recorded as `tutor`. 
    * The student can re-do the questions that he already solved before using *review* system, which is recorded as `in_review`. 

    
* `user_answer` is recorded when `action_type` is `respond`, which stands for the student's submitted answer. It is one of the alphabets `a`, `b`, `c`, and `d`. 
* `platform` shows where the student used *Santa*, which is either **mobile** or **web**. 


#### Example
| timestamp     | action\_type | item\_id | source    | user\_answer | platform |
|---------------|--------------|----------|-----------|--------------|----------|
| 1358114668713 | enter        | b4957    | diagnosis |              | mobile   |
| 1358114691713 | respond      | q6425    | diagnosis | c            | mobile   |
| 1358114701104 | respond      | q6425    | diagnosis | d            | mobile   |
| 1358114712364 | submit        | b4957    | diagnosis |              | mobile   |
| 1358114729868 | enter        | b5180    | sprint |              | mobile   |
| 1358114745592 | respond      | q6815    | sprint    | c            | mobile   |
| 1358114748023 | respond      | q6816    | sprint    | a            | mobile   |
| 1358114748781 | respond      | q6814    | sprint    | a            | mobile   |
| 1358114751032 | submit        | b5180    | sprint |              | mobile   |

### KT3
> Download a `.zip` file from [bit.ly/ednet-kt3](http://bit.ly/ednet-kt3)

|Specification| |
|----|---|
| Size of the compressed file | 0.8GB(762.8MB) |
| Size of the uncompressed file | 4.3GB |
| The number of files | 297,915 |

#### Structure
In *Santa*, a student may participate in various learning activities aside from solving questions, such as reading through experts' commentary on a question or watching lectures provided by the system. EdNet-KT3 incorporates such learning activities by adding the following actions to the EdNet-KT2 dataset. Such actions can be utilized by to infer the impact of learning activities to each student's knowledge state. For example, one may analyze the time each student have spent studying a given material by subtracting the `timestamp`s of `enter` and `quit` actions and use this to study the effect of students' different learning behaviors.


#### Description
As we said above, *explanations* and *lectures* are added. 
* Reading Explanations
    * After each student solves given questions, corresponding explanations are given to him. The sources of explanations for questions from `sprint` and `review` are recorded as `after_sprint` and `after_review`, respectively. One can also re-read explanations of questions that he solved from `my_note`.
    * Whenever a student enters the explanation view in *Santa* UI or exits the view, a corresponding action of type `enter` and `quit` with explanation ID as `item_id` is recorded. Note that the explanation ID is exactly same as the bundle ID. 
* Watching Lectures
    * There are two possible sources that the student can watch a lecture: `archive`, `adaptive_offer`, and `todays_recommendatin::lecture`. He can access all the possible lectures from `archive`. Also, *Santa* can suggest lectures by *Today's recommendation* or *adaptive offer* along with questions. 
    * Whenever a student plays a lecture video or stops watching the video, a corresponding action of type `enter` and `quit` with lecture ID as `item_id` is recorded.

#### Example

| timestamp     | action\_type          | item\_id | source          | user\_answer | platform |
|---------------|-----------------------|----------|-----------------|--------------|----------|
| 1573364188664 | enter                 | b790     | sprint                |              | mobile   |               
| 1573364206572 | respond               | q790     | sprint          | b            | mobile   |               
| 1573364209673 | respond               | q790     | sprint          | d            | mobile   |               
| 1573364209710 | submit                 | b790     | sprint                |              | mobile   |               
| 1573364209745 | enter                 | e790     | sprint             |              | mobile   |               
| 1573364218306 | quit                 | e790     | sprint                |              | mobile   |               
| 1573364391205 | enter                 | l540     | adaptive\_offer   |              | mobile   |               
| 1573364686796 | quit                 | l540     | adaptive\_offer                |              | mobile   |               
| 1573364693793 | enter                 | b6191    | adaptive\_offer               |              | mobile   |               
| 1573364702213 | respond               | q8840    | adaptive\_offer | c            | mobile   |               
| 1573364705838 | submit                 | b6191    | adaptive\_offer                |              | mobile   |               



### KT4
> Download a `.zip` file from [bit.ly/ednet-kt4](http://bit.ly/ednet-kt4)

|Specification| |
|----|---|
| Size of the compressed file | 1.2GB |
| Size of the uncompressed file | 6.4GB |
| The number of files | 297,915 |

#### Structure
In EdNet-KT4, a complete list of actions collected by *Santa* is provided. In particular, the following types of actions are added to EdNet-KT3: `erase_choice`, `undo_erase_choice`, `play_audio`, `pause_audio`, `play_video`, `pause_video`,  `pay`, `refund`, and `enroll_coupon`.
#### Description
* `erase_choice`, `undo_erase_choice`
    * For user's convenience, a student can hide an answer choice by erasing it. He can also undo his  action to consider the choice again. The act of erasing a choice and undoing it are given as actions of type `erase_choice` and `undo_erase_choice` respectively. The answer choice erased/un-erased is supplied in the `user_answer` column.
* `play_audio`, `pause_audio`, `play_video`, `pause_video`
    * A student can play or pause a given multimedia asset. For videos, he can also navigate to different moments of the video by moving his cursor to different places. Such actions are denoted as one of the action types `play_audio`, `pause_audio`, `play_video` or `pause_video`. A column `cursor_time` is added to EdNet-KT4, to represent the moment where he has played or paused the media. 
* `pay`, `refund`
    * By default, a free user is offered 10 questions of Part 2 and 5 each daily. By purchasing a payment item, the student have full access to questions of all parts. A table of payment items is provided separately (see below). Items of type `pass` allows solving all questions for the time `duration` in milliseconds. Items of type `paygo` allows student to solve the specific number of bundles denoted by column `number_of_bundles`.
* `enroll_coupon`
    * A student may enter his promotion coupon code to receive corresponding benefits. The ID of his coupon and the time he entered the coupon is recorded as an action of type `enroll_coupon`. A table of coupons is provided separately (see below). 
    
#### Example

| timestamp     | action\_type      | item\_id | cursor\_time |source | user\_answer | platform |
|---------------|-------------------|----------|--------|--------------|--------------|----------|
| 1358114668713 | pay               | p25      |        |              |              | mobile   |
| 1358114691713 | enter             | b878     | |sprint |                            | mobile   |
| 1358114701104 | text\_enter       | q878     | |sprint |                            | mobile   |
| 1358114712364 | play\_audio       | q878     | 0 |sprint |                         | mobile   |
| 1358114729868 | pause\_audio      | q878     | 10000|sprint |                   | mobile   |
| 1358114745592 | eliminate\_choice | q878     | |sprint | a                      | mobile   |
| 1358114748023 | respond           | q878     | |sprint | c                       | mobile   |
| 1358114748781 | submit            | b878     | |sprint       |                         | mobile   |
| 1358114751032 | enter             | e878     | |sprint    |                            | mobile   |
| 1358114779211 | play\_audio       | e878     | 0|sprint        |                       | mobile   |
| 1358114792300 | pause\_audio      | e878     | 8000|sprint |                   | mobile   |
| 1358114842195 | quit              | e878     | |sprint        |                      | mobile   |

### Contents
> Download a `.zip` file from [bit.ly/ednet-content](http://bit.ly/ednet-content)

|Specification| |
|----|---|
| Size of the compressed file | 0.6MB |
| Size of the uncompressed file | 0.1MB |
| The number of files | 4 |
 
There are five types of contents that *Santa* serves to students: *questions*, *lectures*, *payment items*, *coupons*, and *scores*.
> *scores* are not released yet. It will be released later.

#### Questions
Question information table contains 7 columns: ``question_id``, ``bundle_id``, ``explanation_id``, ``correct_answer``, ``part``, ``tags``, ``deployed_at``. 
* ``question_id`` is the ID of the question, which is a form of `q{integer}`.
* ``bundle_id`` is the ID  of the bundle containing the question, which is a form of `b{integer}`. Each bundle can contains from 1 to 5 questions. 
* ``explanation_id`` is ID of corresponding explanations (expert's commentaries) for each bundle, which is a form of `e{integer}`. Note that bundle_ids and explanation_ids are the same for every question. 
* `correct_answer` is the correct answer of each question recorded as a character between `a` and `d` inclusively. The number of choices depends on the part of the question: every question that does not belong to part 2 has four choices, and part 2 questions have three.
* `part` is the part of each question. It is an integer from **1** to **7**. 
* `tags` are the expert-annotated tags for each question. It is a list of integers, which has a form of `{integer};{integer};...;{integer}`. 
* `deployed_at` represents the time that each question is started to served in *Santa*, represented as **Unix timestamp in milliseconds**.

##### Example


| question_id | bundle_id | explanation_id | correct_answer | part | tags           | deployed_at   |
|-------------|-----------|----------------|----------------|------|----------------|---------------|
| q2319       | b1707     | e1707          | a              | 3    | 179;53;183;184 | 1571279008033 |
| q2320       | b1707     | e1707          | d              | 3    | 52;183;184     | 1571279009205 |
| q2321       | b1707     | e1707          | d              | 3    | 52;183;184     | 1571279010285 |
| q2322       | b1708     | e1708          | b              | 3    | 52;183;184     | 1571279012823 |
| q2323       | b1708     | e1708          | c              | 3    | 179;52;182;184 | 1571279013890 |
| q2324       | b1708     | e1708          | d              | 3    | 52;183;184     | 1571279014989 |

#### Lectures
Lecture information table contains 5 columns: `lecture_id`, `part`, `tags`, `video_length`, `deployed_at`. 
* `lecture_id` is the ID of the lecture. It is a form of `l{integer}`. 
* `part` is the assigned part of the lecture. It is a single integer from `0` to `7`, where `0` stands for the lecture without any particular part assigned.
* `tags` is the expert-annotated tag for each lecture, which is a single **integer**. The tags that are used for questions and lectures are the same. 
* `video_length` is the running time of the video lecture in **milliseconds**, which is a form of single **integer**. 
* `deployed_at` is the time that each lecture is started to served in *Santa*, represented as **Unix timestamp in milliseconds**.

Note that some lectures'  `tags`, `video_lengths`, and `deployed_at` are not available, and they are recorded as `-1`. 
##### Example


| lecture_id | part | tags | video_length | deployed_at   |
|------------|------|------|--------------|---------------|
| l805       | 5    | 99   | 230000       | 1570426256512 |
| l855       | 0    | 203  | 253000       | 1570425118345 |
| l1259      | 1    | 222  | 359000       | 1570424729123 |
| l1260      | 1    | 220  | 487000       | 1570424738105 |
| l1261      | 1    | 221  | 441000       | 1570424743162 |
| l1262      | 1    | 223  | 587000       | 1570424748780 |


#### Payment items
Payment item information table contains 4 columns: `payment_item_id`, `payment_type`, `duration`, and `number_of_questions`. 
* `payment_item_id` is the ID of the payment. It is a form of `p{integer}`. 
* `payment_type` is the type of the payment, which has two possibilities: `pass` and `paygo`. For `pass`, the student can use *Santa* for the fixed amount of time (for example, 3 months). For `paygo`, the student can solve fixed number of questions (for example, 4000). 
* `duration` is the amount of time that the student can use *Santa* when he/she buy a certain `pass`, which is represented in **milliseconds**. When `payment_type` is `paygo`, this is filled up with `-1`. 
* `number_of_questions` represents the number of questions that the student can solve when he/she buy a certain `paygo`, which is a form of single **integer**. When `payment_type` is `pass`, this is filled up with `-1`. 
##### Example

| payment_item_id | payment_type | duration    | number_of_bundles |
|-----------------|--------------|-------------|-------------------|
| p6              | pass         | 15552000000 | -1                |
| p7              | paygo        | -1          | 4000              |
| p8              | pass         | 10368000000 | -1                |
| p9              | pass         | 31536000000 | -1                |

#### Coupons
Coupon information table consists of 3 columns: `coupon_id`, `coupon_type`, and `duration`. 
* `coupon_id` is the ID of the coupon. It is a form of `c{integer}`.
* `coupon_type` is the type of the coupon. It is a form of `type-{integer}`, where the type ID depends on the source of the coupon.
* `duration` is the amount of time that the student can use *Santa* when he/she use a certain coupon, which is represented in **milliseconds**.
##### Example

| coupon_id | coupon_type | duration    |
|-----------|-------------|-------------|
| c16       | type-1      | 15552000000 |
| c17       | type-2      | 432000000   |
| c18       | type-3      | 1000000     |
| c19       | type-3      | 36000000    |


#### Scores
To be released.

## Contact
If you have any questions or find any issues, please contact research@riiid.co.

## License
The dataset is publicly released under [Creative Commons Attribution-NonCommercial 4.0 International license](https://creativecommons.org/licenses/by-nc/4.0/) for research purposes.
