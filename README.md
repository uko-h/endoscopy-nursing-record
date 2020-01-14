# README

## patientsテーブル
|column|type|options|
|------|----|-------|
|name|string|null: false|
|kana|string|null: false|
|number|integer|null: false, unique: true|
|sex|string|null: false|
|birthday|integer|null: false|

### アソシエーション
- has_many :times
- has_many :vital_signs
- has_many :medications, through: :patients_medications
- has_many :patients_medications


## vital_signsテーブル
|column|type|options|
|------|----|-------|
|blood_pressure|integer|null: false|
|pulse|integer|null: false|
|spo2|integer|null: false|
|rass|integer|null: false|
|treatment|string|null: false|
|patient_id|integer|foreign_key: true, null: false|
|time_id|integer|foreign_key: true, null: false|


### アソシエーション
- belongs_to :patient
- belongs_to :time


## medicationsテーブル
|column|type|options|
|------|----|-------|
|scopolamine_butylbromide|integer|null: false|
|glucagon|integer|null: false|
|diazepam|‎integer|null: false|
|midazolam|integer|null: false|
|sosegon|integer|null: false|
|pethidine|integer|null: false|

### アソシエーション
- has_many :patients, through: :patients_medications
- has_many :patients_medications
- has_many :times, through: :medications_times
- has_many :medications_times


## timesテーブル
|column|type|options|
|------|----|-------|
|before_starting|time|null: false|
|ending_time|time|null: false|
|in_30_minutes|time|null: false|
|in_an_hour|time|null: false|
|patient_id|integer|foreign_key: true, null: false|
|vital_sign_id|integer|foreign_key: true, null: false|

### アソシエーション
- belongs_to :patient
- belongs_to :vital_sign
- has_many :medications, through: :medications_times
- has_many :medications_times


## patients_medicationsテーブル
|column|type|options|
|------|----|-------|
|patient_id|integer|foreign_key: true, null: false|
|medication_id|integer|foreign_key: true, null: false|

### アソシエーション
- belongs_to :patient
- belongs_to :medication


## medications_timesテーブル
|column|type|options|
|------|----|-------|
|medication_id|integer|foreign_key: true, unll: false|
|time_id|integer|foreign_key: true, unll: false|

### アソシエーション
- belongs_to :medication
- belongs_to :time