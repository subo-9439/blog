build.gradle
```gradle

buildscript {
	ext {
		spring = "2.4.1"
		boot = "org.springframework.boot"
		lombok = "org.projectlombok:lombok"
	}
	repositories {
		mavenCentral()
	}
	dependencies {
		classpath("$boot:spring-boot-gradle-plugin:$spring")
	}
}

allprojects {
	group = "com.sb.example"
	version = "1.0.0"

}

subprojects {

	apply plugin: "java"
	apply plugin: boot
	apply plugin: "io.spring.dependency-management"
	apply plugin: "idea"

	repositories {
		mavenCentral()
	}

	configurations {
//        developmentOnly
		runtimeClasspath {
			extendsFrom developmentOnly
		}
	}

	dependencies {
//        developmentOnly("$boot:spring-boot-devtools")
		implementation "$boot:spring-boot-starter-security"
		implementation 'com.fasterxml.jackson.core:jackson-annotations'

		compileOnly lombok
		testCompileOnly lombok
		annotationProcessor lombok
		testAnnotationProcessor lombok

		testImplementation "$boot:spring-boot-starter-test"
	}

	test {
		useJUnitPlatform()
	}

}


["comp", "test", "web"].each {
	def subProjectDir = new File(projectDir, it)
	subProjectDir.eachDir {dir->
		def projectName = ":${it}-${dir.name}"
		project(projectName){
			bootJar.enabled(false)
			jar.enabled(true)
		}
	}
}
["server"].each {
	def subProjectDir = new File(projectDir, it)
	subProjectDir.eachDir {dir->
		def projectName = ":${it}-${dir.name}"
		project(projectName){

		}
	}
}

help.enabled(false)
```



settings.gradle
```gradle

rootProject.name = 'example'

["comp", "test", "web", "server"].each {

    def compDir = new File(rootDir, it)
    if(!compDir.exists()){
        compDir.mkdirs()
    }

    compDir.eachDir {subDir ->

        def gradleFile = new File(subDir.absolutePath, "build.gradle")
        if(!gradleFile.exists()){
            gradleFile.text =
                    """
                    
                    dependencies {
                
                    }
                
                    """.stripIndent(20)
        }
        [
                "src/main/java/com/sb/example",
                "src/main/resources",
                "src/test/java/com/sp/example",
                "src/test/resources"
        ].each {srcDir->
            def srcFolder = new File(subDir.absolutePath, srcDir)
            if(!srcFolder.exists()){
                srcFolder.mkdirs()
            }
        }

        def projectName = ":${it}-${subDir.name}";
        include projectName
        project(projectName).projectDir = subDir
    }
}


```