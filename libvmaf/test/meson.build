if not get_option('enable_tests')
    subdir_done()
endif

test_inc = include_directories('.')

test_context = executable('test_context',
    ['test.c', 'test_context.c'],
    include_directories : [libvmaf_inc, test_inc],
    link_with : libvmaf_rc.get_static_lib(),
    dependencies:[stdatomic_dependency],
)

test_picture = executable('test_picture',
    ['test.c', 'test_picture.c', '../src/picture.c', '../src/mem.c', '../src/ref.c'],
    include_directories : [libvmaf_inc, test_inc, include_directories('../src/')],
    dependencies:[stdatomic_dependency],
)

test_feature_collector = executable('test_feature_collector',
    ['test.c', 'test_feature_collector.c',],
    include_directories : [libvmaf_inc, test_inc, include_directories('../src/feature/')],
)

test_thread_pool = executable('test_thread_pool',
    ['test.c', 'test_thread_pool.c', '../src/thread_pool.c'],
    include_directories : [libvmaf_inc, test_inc, include_directories('../src/')],
    dependencies : thread_lib,
)

test_model = executable('test_model',
    ['test.c', 'test_model.c', '../src/dict.c', '../src/svm.cpp', '../src/unpickle.cpp', '../src/pdjson.c', '../src/read_json_model.c'],
    include_directories : [libvmaf_inc, test_inc, opencontainers_include,
                           include_directories('../src/third_party/ptools/'), include_directories('../src')],
    c_args : vmaf_cflags_common,
    cpp_args : vmaf_cflags_common,
    objects : libptools.extract_all_objects(),
    dependencies : thread_lib,
)

test_predict = executable('test_predict',
    ['test.c', 'test_predict.c', '../src/predict.c', '../src/dict.c',
     '../src/feature/feature_collector.c', '../src/feature/alias.c', '../src/model.c', '../src/svm.cpp',
     '../src/unpickle.cpp', '../src/read_json_model.c', '../src/pdjson.c'],
    include_directories : [libvmaf_inc, test_inc, opencontainers_include,
                           include_directories('../src/third_party/ptools/'), include_directories('../src')],
    c_args : vmaf_cflags_common,
    cpp_args : vmaf_cflags_common,
    objects : libptools.extract_all_objects(),
    dependencies : thread_lib,
)

test_feature_extractor = executable('test_feature_extractor',
    ['test.c', 'test_feature_extractor.c', '../src/mem.c', '../src/picture.c', '../src/ref.c',
     '../src/dict.c', '../src/opt.c'],
    include_directories : [libvmaf_inc, test_inc, include_directories('../src/')],
    dependencies : [math_lib, stdatomic_dependency],
    objects : [
      platform_specific_cpu_objects,
      libvmaf_feature_static_lib.extract_all_objects(),
      libvmaf_rc_feature_static_lib.extract_all_objects(),
      libvmaf_rc_cpu_static_lib.extract_all_objects(),
    ]
)

test_dict = executable('test_dict',
    ['test.c', 'test_dict.c'],
    include_directories : [libvmaf_inc, test_inc, include_directories('../src/')],
)

test_cpu = executable('test_cpu',
    ['test.c', 'test_cpu.c'],
    include_directories : [libvmaf_inc, test_inc, include_directories('../src/')],
    objects : libvmaf_rc_cpu_static_lib.extract_all_objects(),
)

test_ref = executable('test_ref',
    ['test.c', 'test_ref.c', '../src/ref.c'],
    include_directories : [libvmaf_inc, test_inc, include_directories('../src/')],
)

test('test_picture', test_picture)
test('test_feature_collector', test_feature_collector)
test('test_thread_pool', test_thread_pool)
test('test_model', test_model)
test('test_predict', test_predict)
test('test_feature_extractor', test_feature_extractor)
test('test_dict', test_dict)
test('test_cpu', test_cpu)
test('test_ref', test_ref)
