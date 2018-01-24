$ cd /path/to/your/webroot
$ git clone git://git.moodle.org/moodle.git                       (1)
$ cd moodle
$ git branch -a                                                   (2)
$ git branch --track MOODLE_34_STABLE origin/MOODLE_34_STABLE     (3)
$ git checkout MOODLE_34_STABLE                                   (4)

admin/Admin@moodle.1
