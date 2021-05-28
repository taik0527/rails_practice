* Users
  * name: string
  * email: string
  * image: string
  * password_digest: string
  * admin: boolean

* Questions
  * title: string
  * body: text
  * solved: boolean
  * user_id: bigint

* Answers
  * body: text
  * user_id: bigint
  * question_id: bigint
