project (jTeamTalkSpamBot)

find_package (Java)

if (Java_FOUND)

  include (UseJava)

  option (BUILD_TEAMTALK_JTEAMTALKSPAMBOT "Build TeamTalk Anti Spam Bot" ON)

  set (JAVA_SOURCES src/SpamBotSession.java src/WebLogin.java src/Main.java src/TeamTalkServer.java)

  if (BUILD_TEAMTALK_JTEAMTALKSPAMBOT)

    if (BUILD_TEAMTALK_JAR)
      set (TEAMTALKJAR_LIBRARY TeamTalk5JAR)
    else()
      find_jar (TEAMTALKJAR_LIBRARY NAMES TeamTalk5
        PATHS ${CMAKE_CURRENT_LIST_DIR}/../../Library/TeamTalkJNI/libs)
    endif()

    if (NOT TEAMTALKJAR_LIBRARY)
      message("Cannot find TeamTalk5.jar")
    else()
      add_jar (jTeamTalkSpamBot INCLUDE_JARS ${TEAMTALKJAR_LIBRARY}
        ENTRY_POINT Main
        SOURCES ${JAVA_SOURCES})
    endif()
  endif()
endif()
