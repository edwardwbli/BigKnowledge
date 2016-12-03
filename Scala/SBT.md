# SBT project directory  
SBT project is recursive

    hello/              # your build's root project's base directory

    Hello.scala         # a source file in your build's root project
                        #   (could be in src/main/scala too)

    build.sbt           # build.sbt is part of the source code for
                        #   meta-build's root project inside project/;
                        #   the build definition for your build

    project/            # base directory of meta-build's root project

        Build.scala     # a source file in the meta-build's root project,
                        #   that is, a source file in the build definition
                        #   the build definition for your build

        build.sbt       # this is part of the source code for
                        #   meta-meta-build's root project in project/project;
                        #   build definition's build definition

        project/        # base directory of meta-meta-build's root project;
                        #   the build definition project for the build definition

            Build.scala # source file in the root project of
                        #   meta-meta-build in project/project/
