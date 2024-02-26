project('<project name>', 'cpp',
    version : '<version>',
    default_options : [
        'cpp_std=c++20',
        
        'warning_level=3',
        'werror=true',

        'b_lto=true',

        'b_pie=true'
    ]
)

cc = meson.get_compiler('cpp')
cc_id = cc.get_id()
system = host_machine.system()

message(f'system: @system@')

link_args = []

if system == 'linux'
    add_project_arguments(
        '-Wconversion',
        '-Wimplicit-fallthrough',

        '-Wformat=2',
        '-fno-delete-null-pointer-checks',

        '-fstack-clash-protection',
        '-fstack-protector-strong',

        language : 'cpp',
    )

    link_args += [
        '-Wl,-z,nodlopen',
        '-Wl,-z,noexecstack',
        '-Wl,-z,relro',
        '-Wl,-z,now',
    ]

    if get_option('buildtype') == 'debug'
        message('Compiling with -ftrapv and _GLIBCXX_ASSERTIONS')
        
        add_project_arguments(
            '-ftrapv',
            '-D_GLIBCXX_ASSERTIONS',

            language : 'cpp',
        )
    else
        message('Compiling with FORTIFY_SOURCE=3')

        add_project_arguments(
            '-D_FORTIFY_SOURCE=3',

            language : 'cpp'
        )
    endif
endif
