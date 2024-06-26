# Copyright (C) 2020 THL A29 Limited, a Tencent company. All rights reserved.
#
# Licensed under the BSD 3-Clause License (the "License"); you may not use this
# file except in compliance with the License. You may obtain a copy of the
# License at
#
# https://opensource.org/licenses/BSD-3-Clause
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
# WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
# License for the specific language governing permissions and limitations under
# the License.

cc_library(
  name = 'write_mostly',
  hdrs = 'write_mostly.h',
  deps = [
    '//flare/base:align',
    '//flare/base:chrono',
    '//flare/base/thread:thread_local',
  ],
  visibility = ['//flare/base:write_mostly'],
)

cc_library(
  name = 'basic_ops',
  hdrs = 'basic_ops.h',
  deps = [
    ':write_mostly',
  ],
  visibility = ['//flare/base:write_mostly'],
)

cc_test(
  name = 'basic_ops_test',
  srcs = 'basic_ops_test.cc',
  deps = [
    ':basic_ops',
    ':write_mostly',
    '//flare/base:write_mostly',
  ]
)

cc_benchmark(
  name = 'write_mostly_benchmark',
  srcs = 'write_mostly_benchmark.cc',
  deps = [
    ':basic_ops',
    ':write_mostly',
    # Tests workaround for gperftools's false-sharing issue.
    '//thirdparty/gperftools:tcmalloc_minimal',
  ]
)

cc_library(
  name = 'metrics',
  hdrs = 'metrics.h',
  srcs = 'metrics.cc',
  deps = [
    ':write_mostly',
    '//flare/base:align',
    '//flare/base:chrono',
    '//flare/base/internal:time_keeper',
    '//flare/base/thread:spinlock',
    '//thirdparty/googletest:gtest_prod',
  ],
  visibility = ['//flare/base:write_mostly'],
)

cc_benchmark(
  name = 'metrics_benchmark',
  srcs = 'metrics_benchmark.cc',
  deps = [
    ':metrics',
  ]
)

cc_test(
  name = 'metrics_test',
  srcs = 'metrics_test.cc',
  deps = [
    ':metrics',
    '//flare/base:write_mostly',
    '//flare/testing:main',
  ]
)
