# Django RQ Scheduler 2

Provides an admin for using `rq-scheduler` with `Django`. Based on https://github.com/TristanH/django-rq-scheduler which is an excellent fork of the original https://github.com/isl-x/django-rq-scheduler.

## Requirements

`django-rq-scheduler-2` depends on the following packages:

* django >= 2
* django-model-utils >= 2.4
* django-rq >= 0.9.3 (`django-rq` requires `RQ` >= 0.5.5)
* rq-scheduler >= 0.6.0
* pytz >= 2015.7
* croniter >= 0.3.24

Testing also requires:

* factory_boy >= 2.6.1
* psycopg2 >= 2.6.1

## Usage

### Install

#### Latest stable version

```sh
pip install django-rq-scheduler-2
```

#### Latest dev version

```sh
pip install git+https://github.com/themotleyfool/django-rq-scheduler.git@master#egg=django-rq-scheduler-2
```

### Update Django Settings

1. Add `django_rq` and `django_rq_scheduler_2` to `INSTALLED_APPS` to `settings.py`:

```python
	INSTALLED_APPS = [
    	...
    	"django_rq",
    	"django_rq_scheduler_2",
    	...
	]
```

2. Configure Django RQ (https://github.com/ui/django-rq#installation).


### Migrate

The last step is migrate the database:

```sh
./manage.py migrate
```

## Creating a job with `django-rq`

See http://python-rq.org/docs/jobs/ or https://github.com/ui/django-rq#job-decorator

An example:

**myapp.jobs.py**

```python
    @job
    def count():
        return 1 + 1
```

## Scheduling a job

### Scheduled job

1. Sign into the Django Admin site, http://localhost:8000/admin/ and locate the **Django RQ Scheduler** section.
2. Click on the **Add** link for Scheduled Job.
3. Enter a unique name for the job in the **Name** field.
4. In the **Callable** field, enter a Python dot notation path to the method that defines the job. For the example above, that would be `myapp.jobs.count`
5. Choose your **Queue**. Side note: The queues listed are defined in the Django settings.
6. Enter the time the job is to be executed in the **Scheduled time** field. Side note: enter the date via the browser's local timezone, the time will automatically convert UTC.
7. Click the **Save** button to schedule the job.

### Repeatable job

1. Sign into the Django Admin site, http://localhost:8000/admin/ and locate the **Django RQ Scheduler** section.
2. Click on the **Add** link for Repeatable Job
3. Enter a unique name for the job in the **Name** field.
4. In the **Callable** field, enter a Python dot notation path to the method that defines the job. For the example above, that would be `myapp.jobs.count`
5. Choose your **Queue**. Side note: The queues listed are defined in the Django settings.
6. Enter the time the first job is to be executed in the **Scheduled time** field. Side note: Enter the date via the browser's local timezone, the time will automatically convert UTC.
7. Enter an **Interval**, and choose the **Interval unit**. This will calculate the time before the function is called again.
8. In the **Repeat** field, enter the number of time the job is to be ran. Leaving the field empty, means the job will be scheduled to run forever.
9. Click the **Save** button to schedule the job.


### Cron job

1. Sign into the Django Admin site, http://localhost:8000/admin/ and locate the **Django RQ Scheduler** section.
2. Click on the **Add** link for Cron Job.
3. Enter a unique name for the job in the **Name** field.
4. In the **Callable** field, enter a Python dot notation path to the method that defines the job. For the example above, that would be `myapp.jobs.count`
5. Choose your **Queue**. Side note: The queues listed are defined in the Django settings.
6. Enter the cron schedule expression for when the job is to be executed in the **Cron string** field. Side note: https://crontab.guru/ might be useful to validate the cron string.
7. Click the **Save** button to schedule the job.

## Reporting issues or features

Please report issues via [GitHub Issues](https://github.com/themotleyfool/django-rq-scheduler-2/issues).
