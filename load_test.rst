Load testing
=========================

Setup
------

Both integration test and load test will need codatlas binaries are
saved somewhere in file system. The default location is
``~/lambda_home``. It could be overriden by setting the environment
variable ``LAMBDA_HOME``.


Integration test
-----------------

We use ``pyresttest`` for integration test and ``requests`` for
sending http requests. To setup, run:
``pip install pyresttest``, ``pip install request``

Then in ``benchmark`` folder, run:
``python integration_test_driver.py``

Load test
----------

We use ``locust`` for load testing and ``requests`` for sending http
requests. To setup, run:
``pip install locustio``, ``pip install request``

Then in ``benchmark`` folder, run:
``python editorserver_load_test.py``

Report
------

Latency report
--------------

::

    | Name                                                                                                           | # reqs | # fails  | Avg(ms) | Min(ms) | Max(ms) | Median(ms) |
    | GET /debugInfo/vJA5SX7phDq3EU-8ltmp2Q__                                                                        | 43     | 0(0.00%) | 7       | 5       | 19      | 6          |
    | GET /member/vJA5SX7phDq3EU-8ltmp2Q__/org.yinwang.pysonar.ast.ListComp                                          | 34     | 0(0.00%) | 13      | 9       | 18      | 12         |
    | GET /metadata/vJA5SX7phDq3EU-8ltmp2Q__/src/main/java/org/yinwang/pysonar/ast/ListComp.java                     | 27     | 0(0.00%) | 14      | 12      | 26      | 14         |
    | GET /node/vJA5SX7phDq3EU-8ltmp2Q__/org.yinwang.pysonar.types.ListType.ListType(org.yinwang.pysonar.types.Type) | 27     | 0(0.00%) | 8       | 7       | 17      | 8          |
    | GET /projects/vJA5SX7phDq3EU-8ltmp2Q__                                                                         | 33     | 0(0.00%) | 6       | 4       | 11      | 6          |
    | GET /references/vJA5SX7phDq3EU-8ltmp2Q__/org.yinwang.pysonar.ast.ListComp.generators                           | 36     | 0(0.00%) | 15      | 10      | 79      | 13         |
    | Total                                                                                                          | 200    | 0(0.00%) |         |         |         |            |


Latenct percentile
------------------

::

    Percentage of the requests completed within given times
    | Name                                                                                                           | # reqs | 50%(ms) | 66%(ms) | 75%(ms) | 80%(ms) | 90%(ms) | 95%(ms) | 98%(ms) | 99%(ms) | 100%(ms) |
    | GET /debugInfo/vJA5SX7phDq3EU-8ltmp2Q__                                                                        | 43     | 6       | 7       | 8       | 8       | 10      | 14      | 19      | 19      | 19       |
    | GET /member/vJA5SX7phDq3EU-8ltmp2Q__/org.yinwang.pysonar.ast.ListComp                                          | 34     | 13      | 14      | 15      | 15      | 17      | 18      | 18      | 18      | 18       |
    | GET /metadata/vJA5SX7phDq3EU-8ltmp2Q__/src/main/java/org/yinwang/pysonar/ast/ListComp.java                     | 27     | 14      | 14      | 15      | 15      | 16      | 20      | 26      | 26      | 26       |
    | GET /node/vJA5SX7phDq3EU-8ltmp2Q__/org.yinwang.pysonar.types.ListType.ListType(org.yinwang.pysonar.types.Type) | 27     | 8       | 8       | 9       | 9       | 10      | 11      | 17      | 17      | 17       |
    | GET /projects/vJA5SX7phDq3EU-8ltmp2Q__                                                                         | 33     | 6       | 6       | 7       | 7       | 8       | 9       | 11      | 11      | 11       |
    | GET /references/vJA5SX7phDq3EU-8ltmp2Q__/org.yinwang.pysonar.ast.ListComp.generators                           | 36     | 13      | 14      | 15      | 15      | 15      | 26      | 79      | 79      | 79       |

